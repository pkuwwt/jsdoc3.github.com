---
title: 使用 JSDoc 3 的 命名路径 (namepath)
description: JSDoc 3 命名路径使用指南。
related:
    - about-block-inline-tags.html
    - tags-inline-link.html
---

## JSDoc 3 中的命名路径 (namepath)

当你文档其他位置引用一个当前位置的 JavaScript 变量时，你必须提供一个唯一个标示符来映射道此变量。命名路径 (namepath) 提供了一种实现方法，而且可以将实例成员、静态成员和内部变量区分开。

{% example "JSDoc 3 命名路径基本语法示例" %}

```
myFunction                    // 函数
MyConstructor                 // 构造函数
MyConstructor#instanceMember  // 实例成员
MyConstructor.staticMember    // 静态成员
MyConstructor~innerMember     // 内部成员，注意：JSDoc 2 使用的是短横线
```
{% endexample %}

下面的例子中：一个**实例**方法名为 "say"， 一个**内部**函数名为 "say"， 还有一个**静态**方法也叫 "say"。它们是相互独立的三个完全不同的方法。

{% example "使用文档标签来描述你的代码" %}

```js
/** @constructor */
Person = function() {
    this.say = function() {
        return "我是一个实例。";
    }

    function say() {
        return "我是一个内部函数。";
    }
}
Person.say = function() {
    return "我是静态函数。";
}

var p = new Person();
p.say();      // 我是一个实例函数。
Person.say(); // 我是一个静态函数。
// 此处无法直接访问内部函数
```
{% endexample %}

所以，你需要用三种不同命名路径语法来描述这三个函数：

{% example "使用文档标签来描述你的代码" %}

```
Person#say  // 名为 "say" 的实例方法
Person.say  // 名为 "say" 的静态方法
Person~say  // 名为 "say" 的内部方法
```
{% endexample %}

你可能会好奇，既然内部方法无法在外部访问到，为什么还需要用专门的语法来描述它呢？你说得对，事实上 "~" 语法确实极少使用，不过一种**可能**的情况是：定义内部函数的容器可能会将内部方法的引用返回到容器外面，因此其他地方的代码是有可能用到这个内部方法的。

注意：如果一个构造函数的一个实例成员刚好又是一个构造函数，你可以简单地将多个命名路径串联起来，构成一个更长的命名路径：

{% example "使用文档标签来描述你的代码" %}

```js
/** @constructor */
Person = function() {
    /** @constructor */
    this.Idea = function() {
        this.consider = function(){
            return "hmmm";
        }
    }
}

var p = new Person();
var i = new p.Idea();
i.consider();
```
{% endexample %}

在此例中，为了引用名为 "consider" 的方法，你需要使用下列命名路径：
`Person#Idea#consider`

这种串联方式适用于三种连接符 `# . ~` 的任意组合。

{% example "特例：模块、外部对象和事件。" %}

```js
/** 一个模块。它的名称是 module:foo/bar
 * @module foo/bar
 */
/** 内置的字符串对象。它的名称是 external:String
 * @external String
 */
/** 一个事件。他的名称是 module:foo/bar.event:MyEvent.
 * @event module:foo/bar.event:MyEvent
 */
```
{% endexample %}

命名路径存在一些特殊情况：[@module][module-tag] 名称的前缀为 "module:"，[@external][external-tag] 名称的前缀为 "external:"， [@event][event-tag] 名称的前缀为 "event:"。

{% example "名称中包含特殊字符的对象的命名路径。" %}

```js
/** @namespace */
var chat = {
    /**
     * 通过 {@link chat."#channel"} 来引用此处。
     * @namespace
     */
    "#channel": {
        /**
         * 通过 {@link chat."#channel".open} 来引用此处。
         * @type {boolean}
         * @defaultvalue
         */
        open: true,
        /**
         * 内部引用必须用反斜线来转义。引用此处需使用
         * {@link chat."#channel"."say-\"hello\""}.
         */
        'say-"hello"': function (msg) {}
    }
};

/**
 * 现在我们在 {@link chat."#channel"} 命名空间中定义了一个事件。
 * @event chat."#channel"."op:announce-motd"
 */
```
{% endexample %}

上述示例中，一个命名空间的成员名称中包含 "非常见" 的字符 (短横线、虚线、甚至于引号)。为引用这些成员，你需要将名称至于引号中，比如：chat."#channel"、chat."#channel"."op:announce-motd"，等等。
名称中的内部引用应该用反斜线转义：chat."#channel"."say-\"hello\""。

[event-tag]: tags-event.html
[external-tag]: tags-external.html
[module-tag]: tags-module.html
