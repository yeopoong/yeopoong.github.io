---
layout: post
published: true
title: "[리액트] React 기본"
categories: dev
tags: frontend react
---

> 리액트 기본 예제를 작성하고 빌드 및 실행해 본다.

## 설치 

```
$ npm install
```

## Hello World

`src/App.js`
```j
import React from "react";
import ReactDOM from "react-dom";

if (module.hot) {
    module.hot.accept();
}

ReactDOM.render(
    <div>Hello World</div>, document.getElementById("app")
);
```

`index.html`
```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title>Todo</title>
</head>
<body>
    <div id="app"></div>
    <script src="./dist/bundle.js"></script>
</body>
</html>
```

## 빌드

`package.json`
```json
"scripts": {
	"build": "./node_modules/.bin/webpack --config webpack.config.js",
	"watch": "./node_modules/.bin/webpack --config webpack.config.js --watch",
	"devserver": "./node_modules/.bin/webpack-dev-server --config webpack.dev.config.js"
},
```

```
$ npm run build

> react_todo@1.0.0 build C:\dev\react\todo_react
> webpack --config webpack.config.js
```