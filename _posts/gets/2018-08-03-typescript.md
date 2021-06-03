---
layout: post
title: "TypeScript"
categories: gets
tags: nodejs typescript 
---

> 타입스크립트 설치 및 기본예제 

## 타입스크립트 컴파일러 설치

```
$ npm install -g typescript
$ tsc -v
Version 3.0.1
```

## 타입스크립트 업데이트
```
$ npm outdated -g typescript
```

```
$ npm uninstall -g typescript
$ npm cache clean
$ npm install -g typescript
```

## Hello Example

`src/hello.ts`
```javascript
let hello: string = "Hello TypeScript!"
console.log(hello);
```

```
$ tsc hello.ts
```

`src/hello.js`
```
$ cat hello.js
var hello = "Hello TypeScript!";
console.log(hello);
```

```
$ node hello.js
Hello TypeScript!
```
