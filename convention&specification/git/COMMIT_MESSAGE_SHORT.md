# 注释规范

## 首先

1. 第一行应该少于50个字
1. 使用 fix, add, change 而不是 fixed, added, changed
1. 永远别忘了第 2 行是空行

## Angular 规范的 Commit message 格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```txt
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。

### Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

**type** 用于说明 commit 的类别，只允许使用下面 **7** 个标识。

* **feat** 新功能（feature）
* **fix** 修补bug
* **docs** 文档（documentation）
* **style** 格式（不影响代码运行的变动）
* **refactor** 重构（即不是新增功能，也不是修改bug的代码变动）
* **test** 增加测试
* **chore** 构建过程、辅助工具的变动
* **perf** 提高性能

如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

subject 是 commit 目的的简短描述，不超过50个字符。

* 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
* 第一个字母大写
* 结尾不加句号

### Body

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

```txt
More detailed explanatory text, if necessary.  Wrap it to
about 72 characters or so.

Further paragraphs come after blank lines.

- Bullet points are okay, too
- Use a hanging indent
```

### Footer

Footer 部分只用于不兼容变动和关闭 Issue。
