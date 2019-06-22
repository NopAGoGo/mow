# 提交信息

## 为什么要关注提交信息

1. 加快 Reviewing Code 的过程

2. 帮助我们写好 release note

3. 5年后帮你快速想起来某个分支，tag 或者 commit 增加了什么功能，改变了哪些代码

4. 让其他开发者在运行 `git blame` 的时候想跪谢

5. 提高项目的整体质量

## 基本要求

1. 第一行应该少于50个字。**随后是一个空行**第一行的题目也可以写成：`Fix issue #8976`

2. 永远不在 `git commit` 上增加 `-m <msg>` 或 `--message=<msg>` 参数，而单独写提交信息

   一个不好的例子： `git commit -m "Fix login bug"`

3. 注释最好包含一个连接指向项目的 issue/story/card。一个完整的连接比一个 issue numbers 更好

## 注释要回答如下信息

### 为什么这次修改是必要的

告诉 Reviewers，提交包含什么改变。

### 如何解决的问题

不是说技术细节，例如：

```txt
Introduce a red/black tree to increase search speed
```

```txt
Remove <troublesome gem X>, which was causing <specific description of issue introduced by gem>
```

### 这些变化可能影响哪些地方

这是最需要回答的问题。因为它会帮你发现在某个 branch 或 commit 中的做了过多的改动。一个提交尽量只做1，2个变化。

你的团队应该有一个自己的行为规则，规定每个 commit 和 branch 最多能含有多少个功能修改。

## 小提示

1. 使用 fix, add, change 而不是 fixed, added, changed
2. 永远别忘了第 2 行是空行
3. 用 Line break 来分割提交信息，让它在某些软件里更易读
4. 请将每次提交限定于完成一次逻辑功能。并且可能的话，适当地分解为多次小更新。

## 例子

```txt
Fix bug where user can't signup.

[Bug #2873942]

Users were unable to register if they hadn't visited the plans
and pricing page because we expected that tracking
information to exist for the logs we create after a user
signs up.  I fixed this by adding a check to the logger
to ensure that if that information was not available
we weren't trying to write it.
```

```txt
Redirect user to the requested page after login

https://trello.com/path/to/relevant/card

Users were being redirected to the home page after login, which is less
useful than redirecting to the page they had originally requested before
being redirected to the login form.

* Store requested path in a session variable
* Redirect to the stored location after successfully logging in the user
```

## 依赖 Github Issue 的 Commit message 格式

这种工作方式期望团队使用 Github 的 Project 和 Issue 来管理开发任务。这时 Commit message 的 Header 部分应该包含 Issue Number。

```txt
[#123] Diverting power from warp drive to torpedoes
[Closes #123] Torpedoes now sufficiently powered
[Closes #123][#124][#125] Torpedoes now sufficiently powered
```

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

type 用于说明 commit 的类别，只允许使用下面7个标识。

* feat 新功能（feature）
* fix 修补bug
* docs 文档（documentation）
* style 格式（不影响代码运行的变动）
* refactor 重构（即不是新增功能，也不是修改bug的代码变动）
* test 增加测试
* chore 构建过程、辅助工具的变动
* perf 提高性能

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

## 相关工具

Commitizen 是一个撰写合格 Commit message 的工具
