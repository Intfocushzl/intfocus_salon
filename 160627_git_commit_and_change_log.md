- **主题:** git commit 与 change log 规范 
- **目的:** 讨论出一套适应于我们当前阶段、当前规模的内部代码提交规范 
- **时间:** 下周一（16-06-27）17：20 - 18:48
- **地点:** 小会议室
- **人员:** albert、星亮、郁骏、jay

## 讨论约束

无约束的讨论，都是在浪费时间:

- 就当前阶段（未来半年即 2016 年内）、当前团队规模（技术人员 3-5 人）。
- 以讨论出结果为目的。
- 求同存异，不完善的结论也是结论（无定论时继续沙龙讨论）。

## 讨论结果

提交格式: `<type>(<scope>) <subject> // Header` 

- type: 必写，使用以下七个标签: 

    - feat：新功能（feature） 
    - fix：修补 bug 
    - docs：文档（documentation） 
    - style： 格式（不影响代码运行的变动） 
    - refactor：重构（即不是新增功能，也不是修改 bug 的代码变动） 
    - test：增加测试 
    - chore：构建过程或辅助工具的变动 

- scope: 可选，默认值 为 文件名或 app 名 
- subject: 必写，中英文亦可 


----

## 讨论点

基于阮大神的文章[Commit message 和 Change log 编写指南](http://www.ruanyifeng.com/blog/2016/01/commit_message_change_log.html)为基础进行讨论。

## Commit message format

每次提交，`Commit message` 包括三个部分：`Header`，`Body` 和 `Footer`。

    <type>(<scope>) <subject> // Header
    // 空一行
    <body>                    // Body
    // 空一行
    <footer>                  // Footer

### Header

`Header` 部分只有一行，包括三个字段：`type`（必需）、`scope`（可选）和 `subject`（必需）。

1. `type` 用于说明 `commit` 的类别，只允许使用下面 7 个标识。

    1. feat：新功能（feature）【功绩】
    2. fix：修补 bug（为什么不使用过去时 fixed ？）
    3. docs：文档（documentation）
    4. style： 格式（不影响代码运行的变动）
    5. refactor：重构（即不是新增功能，也不是修改 bug 的代码变动）
    6. test：增加测试
    7. chore：构建过程或辅助工具的变动【家务活】

    如果 `type` 为 `feat` 和 `fix`，则该 `commit` 将肯定出现在 `Change log` 之中。其他情况（`docs`、`chore`、`style`、`refactor`、`test`）由你决定，要不要放入 `Change log`，建议是不要。
    
2. scope
 
    `scope` 用于说明 `commit` 影响的范围，比如数据层、控制层、视图层等等，视项目不同而不同。
    
3. subject

    `subject` 是 `commit` 目的的简短描述，不超过 50 个字符。
    
    - 以动词开头，使用第一人称现在时，比如 `change`，而不是 `changed` 或 `changes`
    - 第一个字母小写
    - 结尾不加句号（.）
  
## Body

`Body` 部分是对本次 `commit` 的详细描述，可以分成多行。下面是一个范例。

    More detailed explanatory text, if necessary.  Wrap it to 
    about 72 characters or so. 
    
    Further paragraphs come after blank lines.
    
    - Bullet points are okay, too
    - Use a hanging indent
    
有两个注意点。

1. 使用第一人称现在时，比如使用 `change` 而不是 `changed` 或 `changes`。
2. 应该说明代码变动的动机，以及与以前行为的对比。

## Footer

Footer 部分只用于两种情况。

1. 不兼容变动

    如果当前代码与上一个版本不兼容，则 Footer 部分以 `BREAKING CHANGE` 开头，后面是对变动的描述、以及变动理由和迁移方法。

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
            
2. 关闭 Issue

    如果当前 commit 针对某个 issue，那么可以在 Footer 部分关闭这个 issue 。

        Closes #234
        
    也可以一次关闭多个 issue 。

        Closes #123, #245, #992
       
## Revert

还有一种特殊情况，如果当前 `commit` 用于撤销以前的 `commit`，则必须以 `revert:` 开头，后面跟着被撤销 `Commit` 的 `Header`。

    revert: feat(pencil): add 'graphiteWidth' option

    This reverts commit 667ecc1654a317a13331b17617d973392f415f02.
    
Body 部分的格式是固定的，必须写成 `This reverts commit <hash>.`，其中的 `hash` 是被撤销 `commit` 的 `SHA` 标识符。

如果当前 commit 与被撤销的 commit，在同一个发布（release）里面，那么它们都不会出现在 Change log 里面。如果两者在不同的发布，那么当前 commit，会出现在 Change log 的Reverts小标题下面。