---
layout: post
title: "Classes"
date: 2023-06-02
last_modified_at: 2023-06-02
categories: [Typescript]
---

typescript 객체지향 프로그래밍

```tsx
class Player{
	constructor(
		private firstName:string,
		private lastName:string
		public nickname:string
	){}
}
const nico = new Player("hams", "a","c");
```

보통 자바스크립트에서는 constructor를 만들고 this.이름 처럼 입력해서 구성하는데

타입에서는 파라미터를 쓰기만 하면 알아서 컨스트럭쳐를 만들어준다.

js로 컴파일되면 this.firstName으로 변환된다

```tsx
// js
class Player {
  constructor() {
    this.firstName;
    this.lastName;
    this.nickName;
  }
}
```

객체에 타입이 적용되면 해당 객체는 그 타입의 인스턴스라고 부른다.

타입에서는 private나 public property를 사용하나, 스크립트로 컴파일되면서 없어진다

private는 프로젝트 내에서 변경시키면 안되는 값. 타입이 지켜주고있음

public으로 선언한 것만 된다 ⇒ 이 부분들은 자바스크립트에서는 없는 기능

- ## 생성자 함수의 new 호출을 통한 객체 생성 과정 :
  1. 빈 객체 만들기
  2. 만든 빈 객체를 this코드에 할당
  3. 생성자 함수 바디의 코드를 실행(this에 속성 및 메소드 추가)
  4. 만든 빈 객체의 **\*\*proto**\*\*에 생성자 함수의 prototype 속성 대입
  5. this를 생성자의 반환값으로 변환

## 추상클래스

```tsx
abstract class User{
	constructor(
		private firstName:string,
		private lastName:string
		public nickname:string
	){}
	getFullName(){
		return `${this.firstName} ${this.lastName}`
	}
}

class Player extends User{

}
```

다른 클래스가 상속받을 수 있는 클래스

직접 새로운 인스턴스를 만들 수는 없다.

js는 추상클래스 개념이 없어 컴파일시 추상클래스는 만들어지지 않음

메소드는 클래스 안에 있는 함수를 가리킴

## 추상 메소드

```tsx
abstract getNickName():void
```

추상 메소드는 구현이 되어 있지 않은(코드가 없는)메소드이다.

추상 메서드를 선언했다면 자식 클래스는 해당 메서드를 반드시 구현하도록 강제된다

추상 클래스 안에서 추상 메소드를 만들 수 있으나, 추상 클래스 안에서 메소드를 구현하면 안되기 때문에 콜 시그니쳐를 적어둬야함

추상 메소드는 추상 클래스를 상속받는 모든 것들이 구현을 해야하는 메소드 의미

만약 property를 private로 만들면, 그 클래스를 상속하였더라도 프로퍼티에 접근 불가능 ⇒ 필드가 외부로부터를 보호되지만 자식클래스에서 사용되길 원하면 private가 아닌 protected를 사용. 여전히 바깥에선 접근이 안된다

| 구분      | 선언한 클래스 내 | 상속받은 클래스 내 | 인스턴스 |
| --------- | ---------------- | ------------------ | -------- |
| private   | ⭕               | ❌                 | ❌       |
| protected | ⭕               | ⭕                 | ❌       |
| public    | ⭕               | ⭕                 | ⭕       |

## 해시맵예시

```tsx
// 오브젝트의 type을 선언해야 할 때 사용
type Words = {
  [key: string]: string;
};

class Dict {
  // 프라이빗이 constructor안에 들어갈 수 없기 때문에 이렇게 함
  private words: Words;
  constructor() {
    this.words = {};
  }
  // 클래스를 타입처럼 활용
  add(word: Word) {
    if (this.words[word.term] === undefined) {
      this.words[word.term] = word.def;
    }
  }
  def(term: string) {
    return this.words[term];
  }
  static hello() {
    return "hello";
  }
}

class Word {
  constructor(public readonly term: string, public def: string) {}
}

const hamster = new Word("hamster", "cute animal");
const dict = new Dict();
dict.add(hamster);
```

클래스를 타입처럼 사용할 수 있음. 파라미터가 클래스의 인스턴스이길 원하면 이런 식으로도 쓸 수 있다.

readonly : public으로 보여주고 싶지만 수정을 막고싶을 때 사용
