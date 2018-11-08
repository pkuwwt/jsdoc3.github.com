---
title: JSDoc 的命令行参数
description: 关于 JSDoc 的命令行参数。
related:
    - about-configuring-jsdoc.html
---

JSDoc 的最简单用法为：

    /path/to/jsdoc yourSourceCodeFile.js anotherSourceCodeFile.js ...

其中 `...` 表示需要生成文档的其他代码文件。

此外，你可以提供一个 [Markdown 文件][md-file] 的路径，或者一个名为 "README" 的文件的路径，这会作为生成的文档的首页。参见 [相关指令][including-readme]。

JSDoc 支持大量的命令行选项，其中很多同时具备长短两种形式。除了直接再命令行中指定之外，命令行选项也可以通过[配置文件][config-file]的方式传递给 JSDoc。

这些命令行选项包括：

选项|描述
------|-----------
`-a <value>`, `--access <value>`|只显示具有指定访问属性( `access` )的符号，取值可以为：`private`、 `protected`、 `public` 或 `undefined` 或 `all` (所有访问级别)。默认情况下，除了 `private` 之外的符号都会显示。
`-c <value>`, `--configure <value>`|JSDoc [配置文件][config-file] 的路径。默认为 `conf.json` 或 JSDoc 安装目录中的 `conf.json.EXAMPLE`。
`-d <value>`, `--destination <value>`|生成文档的输出文件夹。对于 JSDoc 内置的 Haruki 模版，使用 `console` 来将数据打印到终端。默认为 `./out`。
`--debug`|显示有助于调试 JSDoc 本身问题的日志信息。
`-e <value>`, `--encoding <value>`|读取所有源码文件时使用此编码。默认是 `utf8`。
`-h`, `--help`|显示 JSDoc 的命令行选项，然后推出。
`--match <value>`|只运行名称中包含 `value` 的测试。
`--nocolor`|当运行测试时，不要再终端输出中使用颜色。在 Windows 中，这个选项默认是打开的。
`-p`, `--private`|在生成的文档中包含用 [`@private` 标签][private-tag] 标记的符号。默认情况下，私有符号不会包含进来。
`-P`, `--package`|`package.json` 文件，此文件中包含了项目名、版本、和其他细节。默认为源码路径中找到的第一个 `package.json` 文件。
`--pedantic`|将所有错误视为致命错误，将警告也视为错误。默认为 `false`。
`-q <value>`, `--query <value>`|一个查询 (query) 格式的字符串，其中的查询变量会存于变量 `env.opts.query` 中。示例：`foo=bar&baz=true`。
`-r`, `--recurse`|递归扫描源码文件和教程的子目录。
`-R`, `--readme`|在生成的文档中包含 `README.md` 文件。默认使用源码路径中找到的第一个 `README.md` 文件。
`-t <value>`, `--template <value>`|用于生成文档的模版文件的路径。默认为 `templates/default`，此为 JSDoc 的内置默认模版。
`-T`, `--test`|运行 JSDoc 的测试集，并将结果打印到终端。
`-u <value>`, `--tutorials <value>`|JSDoc 搜索教程的目录位置。如果省略，将不会生成教程页面。更多信息，参见 [教程指令][tutorials]。
`-v`, `--version`|显示 JSDoc 的版本号，然后退出。
`--verbose`|当 JSDoc 运行时，在终端中打印详细的日志信息。默认为 `false`。
`-X`, `--explain`|将所有的 doclets 以 JSON 格式输出到终端，然后退出。


[config-file]: about-configuring-jsdoc.html
[including-readme]: about-including-readme.html
[md-file]: http://daringfireball.net/projects/markdown/
[private-tag]: tags-private.html
[tutorials]: about-tutorials.html


## Examples

使用配置文件`/path/to/my/conf.json`，为 `./src` 目录中的文件生成文档，然后将输出保存于 `./docs` 目录中。

{% example %}

```
/path/to/jsdoc src -r -c /path/to/my/conf.json -d docs
```
{% endexample %}

运行所有的名称包含 `tag` 的 JSDoc 测试，然后显示每个测试的日志信息：

{% example %}

```
/path/to/jsdoc -T --match tag --verbose
```
{% endexample %}
