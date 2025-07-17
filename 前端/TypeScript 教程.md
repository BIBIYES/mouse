---
number headings: first-level 1, max 6, _.1.1
tags:
  - ts
  - typescript
date: 2025-05-02
---

# TypeScript 教程 1 

## 1 什么是 `TypeScript`

`TypeScript` 是 `JavaScript` 的超集，浏览器本质上还是运行 `javasscript`, 我们需要将 `ts` 编译成 `js` 才能运行  

## 2 静态类型检查

* `typescript` 支持静态类型检查，在代码运行前进行检查，减少运行时的异常出现的几率，此种检查叫做**静态类型检查**
* 同样的功能 `TypeScript` 的代码要大于 `JavaScript`, 但由于 `TypeScipt` 的代码结构更清晰，在后期的项目维护中 `TypeScipt` 的维护效率要远胜于 `JavaScript`

## 3 编译 `Typescript`

浏览器不能直接运行 `ts` 需要将 `ts` 编译成 `js` 才能运行

### 3.1 命令行编译

要使用命令行编译你需要

1. 全局安装 `ts`

```shell
npm install typescript -g
```

2. 编译 `ts`

```shell
tsc index.ts
```

> 由于我们需要常常修改代码，手动编译的方式过于繁琐，因此该方法不常用

## 4 自动编译

1. 输入命令来生成 `tsconfig`

```shell
	tsc --init
```

执行完这个命令后，当前目录会生成一个 `tsconfig.json` 文件，它是一个可配置的 `json` 文件，该文件的用途是，要求 `tsc` 按照 `tsconfig.json` 的配置去编译 `js` 文件

2. 监听 `ts` 文件

```shell
	tsc --watch
```

该命令会监视当前目录的所有文件，如有改动自动编译 `ts` 文件

## 类型

## 类型声明

参考如下变量类型声明的方式

```ts
// 字符串类型
let a: string = "你好";

// 数字类型（整数或浮点数）
let b: number = 100;
let c: number = 3.14;

// 布尔类型
let d: boolean = true;
let e: boolean = false;

// 数组类型（写法一：类型后加 []）
let f: number[] = [1, 2, 3];
// 数组类型（写法二：使用 Array 泛型）
let g: Array<string> = ["a", "b", "c"];

// 元组类型（固定长度和类型的数组）
let h: [string, number] = ["张三", 20];

// 枚举类型
enum Color {
  Red,
  Green,
  Blue
}
let i: Color = Color.Green;

// 任意类型（不推荐使用，除非你确实不确定类型）
let j: any = "可以是字符串";
j = 123;
j = true;

// 空类型（用于函数没有返回值的情况）
function sayHello(): void {
  console.log("你好！");
}

// null 和 undefined 类型
let k: null = null;
let l: undefined = undefined;

// 联合类型（变量可以是几种类型之一）
let m: string | number = "可以是字符串";
m = 123;

// 字面量类型（变量只能是特定几个值）
let n: "男" | "女" = "男";

// 对象类型（可以具体指定结构）
let o: { name: string; age: number } = {
  name: "李四",
  age: 25
};

// 类型别名（自定义类型名）
type User = {
  id: number;
  username: string;
};
let p: User = {
  id: 1,
  username: "小明"
};

// 接口类型（定义对象结构）
interface Animal {
  name: string;
  age: number;
}
let q: Animal = {
  name: "小狗",
  age: 2
};

// 函数类型（指定参数和返回值类型）
let add: (x: number, y: number) => number = function (x, y) {
  return x + y;
};

```

## 类型推断

TypeScript 具有强大的类型推断能力，能够在很多情况下自动推断出变量的类型，而不需要显式地指定类型注解。

列如

```ts
let name = "骆子豪"
name = 1
```

此时编译器会报错。而不需要显示的去指定

```ts
let name: string = "骆子豪"
name = 1
```

同样编译器也会报错