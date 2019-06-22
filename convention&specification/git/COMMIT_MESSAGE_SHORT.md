# Commit message 的格式

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

## 1. Header

Header 部分只有一行，包括三个字段：type（必需）、scope（可选）和 subject（必需）。

### (1) type

type 用于说明 commit 的类别，只允许使用下面7个标识。

* feat 新功能（feature）
* fix 修补bug
* docs 文档（documentation）
* style 格式（不影响代码运行的变动）
* refactor 重构（即不是新增功能，也不是修改bug的代码变动）
* test 增加测试
* chore 构建过程、辅助工具的变动
* perf 提高性能

如果 type 为 feat 和 fix，则该 commit 将肯定出现在 Change log 之中。其他情况（docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。

### (2) scope

scope 用于说明 commit 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。

### (3) subject

subject 是 commit 目的的简短描述，不超过50个字符。

* 以动词开头，使用第一人称现在时，比如 change，而不是 changed 或 changes
* 第一个字母小写
* 结尾不加句号

## 2. Body

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

## 3. Footer

Footer 部分只用于不兼容变动和关闭 Issue。

### (1) 不兼容变动

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

### (2) 关闭 Issue

可以一次关闭多个。

```txt
Closes #123, #245, #992
```

## 4. Revert

还有一种特殊情况，如果当前 commit 用于撤销以前的 commit，则必须以revert:开头，后面跟着被撤销 Commit 的 Header。

```txt
revert: feat(pencil): add 'graphiteWidth' option

This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
```

Body部分的格式是固定的，必须写成This reverts commit \<hash\>.，其中的hash是被撤销 commit 的 SHA 标识符。
