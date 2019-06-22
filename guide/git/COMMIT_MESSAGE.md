# Commit message 编写指南

社区有多种 Commit message 的写法规范。本文介绍 Angular 规范，这是目前使用最广的写法，比较合理和系统化，并且有配套的工具。

## 一、Commit message 的作用

### 1. 提供更多的历史信息，方便快速浏览

比如，下面的命令显示上次发布后的变动，每个 commit 占据一行。你只看行首，就知道某次 commit 的目的。

```txt
git log <last tag> HEAD --pretty=format:%s
```

### 2. 可以过滤某些 commit（比如文档改动），便于快速查找信息

比如，下面的命令仅仅显示本次发布新增加的功能。

```txt
git log <last release> HEAD --grep feature
```

### 3. 可以直接从 commit 生成 Change log

Change Log 是发布新版本时，用来说明与上一个版本差异的文档，详见后文。

## 二、Commit message 的格式

每次提交，Commit message 都包括三个部分：Header，Body 和 Footer。

```txt
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```

其中，Header 是必需的，Body 和 Footer 可以省略。

不管是哪一个部分，任何一行都不得超过72个字符（或100个字符）。这是为了避免自动换行影响美观。

### 1. Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

#### (1) type

**type** 用于说明 commit 的类别，只允许使用下面7个标识。

* **feat** 新功能（feature）
* **fix** 修补bug
* **docs** 文档（documentation）
* **style** 格式（不影响代码运行的变动）
* **refactor** 重构（即不是新增功能，也不是修改bug的代码变动）
* **test** 增加测试
* **chore** 构建过程、辅助工具的变动
* **perf** 提高性能

如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

#### (2) scope

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

#### (3) subject

subject 是 commit 目的的简短描述，不超过50个字符。

* 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
* 第一个字母小写
* 结尾不加句号

### 2. Body

Body 部分是对本次 commit 的详细描述，可以分成多行。下面是一个范例。

```txt
More detailed explanatory text, if necessary.  Wrap it to
about 72 characters or so.

Further paragraphs come after blank lines.

- Bullet points are okay, too
- Use a hanging indent
```

有两个注意点。

1. 使用第一人称现在时，比如使用 change 而不是 changed 或 changes
1. 应该说明代码变动的动机，以及与以前行为的对比

### 3. Footer

Footer 部分只用于不兼容变动和关闭 Issue。

#### (1) 不兼容变动

如果当前代码与上一个版本不兼容，则 Footer 部分以 BREAKING CHANGE 开头，后面是对变动的描述、以及变动理由和迁移方法。

```txt
BREAKING CHANGE: isolate scope bindings definition has changed.

    To migrate the code follow the example below:

    Before:

    scope: {
      myAttr: 'attribute',
    }

    After:

    scope: {
      myAttr: '@',
    }

    The removed `inject` wasn't generaly useful for directives so there should be no code using it.
```

#### (2) 关闭 Issue

可以一次关闭多个。

```txt
Closes #123, #245, #992
```

### 4. Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

```txt
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成This reverts commit \<hash\>.，其中的hash是被撤销 commit 的 SHA 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。

## 三、相关工具

Commitizen 是一个撰写合格 Commit message 的工具。

## 五、生成 Change log

如果你的所有 Commit 都符合 Angular 格式，那么发布新版本时， Change log 就可以用脚本自动生成，详情略。
