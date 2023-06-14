---
layout: post
title: "polymorphis"
date: 2023-06-14
last_modified_at: 2023-06-14
categories: [Typescript]
---

다른 모양의 코드를 가질 수 있게 하는것
타입이 초기에 결정되는 것이 아닌, 사용할 때 결정되는 것

placeholder type → generic

```jsx
interface SStorage<T>{
	// key가 제한되지 않은 오브젝트를 정의하게 해 줌
	[key:string] : T
}

class LocalStorage<T>{
	private storage : SStorage<T> = {}
	set(key:string, value:T){
		this.storage[key] = value;
	}
	remove(key:string){
		delete this.storage[key]
	}
	get(key:string):T{
		return this.storage[key]
	}
	clear(){
		this.storage = {}
	}
}

const stringStorage = new LocalStorage<string>()
```

localStorage클래스를 초기화할 때, 타입스크립트에게 T라고 불리는 제네릭을 받을 계획이라고 미리 알림

#### 과정

⇒ generic이 클래스 이름에 들어오고 ⇒ 같은 generic을 인터페이스로 보내줌 ⇒ 인터페이스가 제네릭을 받음 ⇒ 제네릭을 내보낼 것이라고 이야기
