---
layout: post
title: "error 모음"
date: 2023-04-11
last_modified_at: 2023-04-11
categories: [Jekyll]
---

<br><br>
ios 환경에서 Jekyll 블로그를 만들어보면서

테마 적용이나 설치에 있어 난관에 봉착한 횟수가 수도 없었기에,

미래의 나를 위해서라도 이렇게 마주했던 에러와 그 대처법을 적어둔다.
<br><br>

---

<br>
## Gem::FilePermissionError

```bash
$ gem install bundler
You don't have write permissions for ... (Gem::FilePermissionError)
You don't have write permissions for the /Library/Ruby/Gems/2.3.0 directory.
```

gem install 실행 시 발생하는 에러.
찾아본 결과, 시스템 ruby를 이용하고 있기 때문에 권한이 없어 gem 설치가 안된 것이라고 한다.
<br><br>

**해결 방법**

```bash
brew update
brew install rbenv ruby-build
```

ruby를 업데이트 한다

```bash
rbenv versions
```

ruby가 잘 설치되었는지 확인한다

```bash
rbenv install -l
```

rbenv로 관리되는 Ruby를 설치해야 하기 때문에,
설치 가능한 버전들을 확인한다

```bash
rbenv install <version>
```

설치!!

```bash
rbenv versions
```

```bash
rbenv global <version>
```

버전을 확인한 후에 rbenv로 글로벌 버전을 변경한다

```bash
vim ~/.zshrc
```

```bash
[[ -d ~/.rbenv  ]] && \
  export PATH=${HOME}/.rbenv/bin:${PATH} && \
  eval "$(rbenv init -)"
```

rbenv PATH를 추가하기 위해 본인의 쉘 설정 파일 (..zshrc, .bashrc) 을 열어 다음의 코드를 추가

```bash
source ~/.zshrc
```

source로 코드를 적용한다

```bash
gem install bundler
```

gem install 실행

\+

나같은 경우엔 flutter를 설치하면서 zshrc파일을 건드릴 일이 있었는데,

그 과정에서 뭔가 틀어졌었던 것 같다.
