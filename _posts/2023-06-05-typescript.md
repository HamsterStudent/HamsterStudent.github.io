---
layout: post
title: "Interfaces"
date: 2023-06-05
last_modified_at: 2023-06-05
categories: [Typescript]
---

Interface는 type과 비슷하지만 두가지가 다름

type는 오브젝트의 모양을 알려주는데 쓸 수 있고, 타입이 어떤 형식인지 알려줄 때 쓰일 수 있음

```tsx
type Team = "red" | "blue" | "yellow";
type Health = 1 | 5 | 10;

type Player = {
  nickname: string;
  team: Team;
  health: Health;
};

const nico: Player = {
  nickname: "nico",
  team: "read",
  health: 120,
};
```

타입을 지정된 옵션으로만 사용하게 만드는 방법

```tsx
interface Player{
	nickname:string,
	team:Team,
	health:Health,
}

// 잘못된 용법. 이렇게 쓰면 작동 안함
interface Hello = string
```

interface는 오브젝트의 모양을 특정해주기 위한 용도이다

타입스크립트에게 오브젝트의 모양을 알려주는 방법엔 type를 쓰는 것과 interface를 쓰는 방법 두가지가 있다. 같은 역할을 하지만 type는 interface에 비해 활용할 수 있는 것이 더 많음

interface는 오로지 '오브젝트'의 모양을 타입스크립트에 설명해 주기 위해서만 사용된다.

```tsx
interface User {
	name:string
	//readonly를 사용할 수도 있음
	readonly nickname : string
}

interface Player extends User{
}

const nico : Player = {
	name : "nico"
	nickname : "hamster"
}
```

interface 용법

```tsx
type User = {
  name: string;
  readonly nickname: string;
};
type Player = User & {};

const nico: Player = {
  name: "nico",
};
```

type 용법

인터페이스의 또 다른 특징으로는 property들을 축적시킬 수 있다는 데 있다.

```tsx
interface User {
  name: string;
}
interface User {
  lastname: string;
}
interface User {
  health: number;
}

const nico: User = {
  name: "nico",
  lastname: "las",
  health: 123,
};
```

인터페이스를 각각 만들기만 하면 타입스크립트가 알아서 합쳐준다. type는 이렇게 할 수 없음

## type과 interface 섞어쓰기

```tsx
abstract class User {
  constructor(protected firstName: string, protected lastName: string) {}
  abstract sayHi(name: string): string;
  abstract fullName(): string;
}

class Player extends User {
  sayHi(name: string) {
    return `Hello ${name}. My name is ${this.fullName()}`;
  }
  fullName() {
    return `${this.firstName} ${this.lastname}`;
  }
}
```

추상 클래스는 상속받는 다른 클래스가 가질 property와 메소드를 지정하도록 해줌

protected는 추상 클래스로부터 상속받은 클래스들이 property에 접근하도록 해줌

추상클래스는 만들면 js로 컴파일되면서 결국 일반 클래스로 변한다 ⇒ 표준화된 property와 method를 갖도록 해주는 청사진을 만들기 위해 추상클래스 사용. 일반 클래스로 변경되는 것은 의미가 없음

⇒ interface는 컴파일하면 js로 바뀌지 않고 사라짐

⇒ interface를 쓸 때 클래스가 특정 형태를 따르도록 어떻게 강제하는가?

```tsx
interface User {
  firstName: string;
  lastName: string;
  fullName(): string;
  sayHi(name: string): string;
}

interface Human {
  health: number;
}

class Player implements User, Human {
  constructor(
    public firstName: string,
    public lastName: string,
    public health: number,
  ) {}
  sayHi(name: string) {
    return `Hello ${name}. My name is ${this.fullName()}`;
  }
  fullName() {
    return `${this.firstName} ${this.lastname}`;
  }
}
```

implements : interface에서 extend대신 쓰는 것

interface는 여러 개 상속받을수도 있다.

단점

1. 인터페이스를 상속할 때에는 property를 private로 사용하지 못함
2. constructor를 써줘야 함

## interface를 type으로 지정하기

```tsx
interface User {
  firstName: string;
  lastName: string;
  fullName(): string;
  sayHi(name: string): string;
}

function makeUser(user: User) {
  return "hi";
}
makeUser({
  firstName: "nico",
  lastName: "las",
  fullName: () => "xx",
  sayHi: (name) => "string",
});
```

내보내는 내용의 타입을 지정할수도 있다

```tsx
interface User {
  firstName: string;
  lastName: string;
  fullName(): string;
  sayHi(name: string): string;
}

function makeUser(user: User): User {
  return {
    firstName: "nico",
    lastName: "las",
    fullName: () => "xx",
    sayHi: (name) => "string",
  };
}
```

## Recap

```tsx
type PlayerA = {
	name: string
}
type PlayerAA = PlayerA & {
	lastName:string
}
const playerA:PlayerAA = {
	name:"nico"
	lastName: "xxx"
}

interface PlayerB{
	name: string
}
interface PlayerBB extends PlayerB {
	lastname:string
}
interface PlayerBB{
	health:number
}
const playerB:PlayerBB = {
	name:"nico",
	lastName: "xxx"
}
```

```tsx
type PlayerA = {
  firstName: string;
};
interface PlayerB {
  firstName: string;
}

class User implements PlayerB {
  constructor(public firstName: string) {}
}
```

type도 implements를 사용할 수 있다.

타입스크립트 커뮤니티에서는 대체로 클래스나 오브젝트의 모양을 정의하고 싶으면 interface,

다른 경우에는 type를 사용하기를 권장.

type는 새 property를 추가하기 위해 다시 선언될 수 없지만, interface는 항상 상속이 가능함

[Documentation - Everyday Types](https://www.typescriptlang.org/docs/handbook/2/everyday-types.html#differences-between-type-aliases-and-interfaces)
