# GitHub上的markdown格式一些示例示
> 具体的参考[果冻虾仁的文章]（https://github.com/guodongxiaren/README）

GitHub上不支持[TOC]

想要目录可以这样实现

[First](#First)
[111](##F1)


##First
###F1
###F2
##Second
###S1
###S2

考虑这样的目录结构：

    project
        ├── widget
        │   ├── a
        │   │   ├── a.css
        │   │   ├── a.js
        │   │   └── a.php
        │   ├── b
        │   │   ├── b.css
        │   │   ├── b.js
        │   │   └── b.php
        │   └── c
        │       ├── c.css
        │       ├── c.js
        │       └── c.php
        ├── bootstrap.css
        ├── bootstrap.js
        ├── index.php
        └── jquery.js

# 前面空四个空格
    雕刻技法l
        快乐记得了
        
# 流程图变横向

```flow
op1=>operation: My Ope
op2=>operation: My Ope
op3=>operation: My Ope

op1(right)->op2(right)->op3
```


```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```
