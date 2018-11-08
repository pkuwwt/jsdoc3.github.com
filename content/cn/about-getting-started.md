---
title: 开始使用 JSDoc 3
description: 用 JSDoc 为 JavaScript 代码编写文档快速指南。
---

## 开始使用

JSDoc 3 是一种 JavaScript 的 API 文档生成器，类似于 Javadoc 或 phpDocumentor。通过这一类工具，你可以在代码附近的注释中直接添加文档。而 JSDoc 工具可以扫描你的代码，然后生成一个 HTML 格式的文档网站。

## 为你的代码添加文档注释

JSDoc 的目的是为你的 JavaScript 应用或代码库生成 API 文档。如果你希望为你的代码添加文档，包括代码中的模块、命名空间、类、方法、方法的参数等等，那么 JSDoc 将满足你的需求。

JSDoc 注释一般直接放在待描述的代码之前。每个注释必须以序列 `/**` 开头，以便于 JSDoc 解析器正确识别。
以 `/*`、`/***` 或更多星号开头的注释将会被忽略。这算是 JSDoc 提供的一种功能，有助于减少需要解析的注释块。

{% example "最简单的文档为一句话描述" %}

```js
/** 这是 foo 函数的一个描述。 */
function foo() {
}
```
{% endexample %}

添加描述非常简单：再文档注释中加入描述语言即可。

特殊的 "JSDoc 标签" 用于提供更多信息。比如，如果当前函数是某个类的构造函数，你可以用 `@constructor` 标签来标示。

{% example "使用 JSDoc 标签来描述代码" %}

```js
/**
 * 表示一本书。
 * @constructor
 */
function Book(title, author) {
}
```
{% endexample %}

还有很多其它种类的标签可用于添加更多信息。参见 [主页][block-tags] 中 JSDoc 3 支持的完整的标签列表。

{% example "通过标签添加更多信息" %}

```js
/**
 * 表示一本书。
 * @constructor
 * @param {string} title - 此书的标题。
 * @param {string} author - 此书的作者。
 */
function Book(title, author) {
}
```
{% endexample %}

[block-tags]: index.html#block-tags

## 生成一个网站

一旦你的代码注释好了，你可以用 JSDoc3 工具来从源码中生一个 HTML 网站。
source files.

默认情况下，JSDoc 使用内置的 "默认" 模版来将文档转换为 HTML。你可以编辑这个模版来满足你的需求，当然，必要时你也可以创建一个全新的模版。

{% example "在命令行中运行文档生成器" %}

```
jsdoc book.js
```
{% endexample %}

此命令将再当前目录中生成一个名为 `out/` 的文件夹，此文件夹中保存有生成的 HTML 页面。

