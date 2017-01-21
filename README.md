GitHub上的markdown格式一些利于排版的用法
=======================================
> 想全面了解的可以参考[果冻虾仁的文章]（https://github.com/guodongxiaren/README）

##目录的实现
GitHub上不支持[TOC]

想要目录可以这样实现

```
##目录
* [xxx](#First)
    * [yyy](#F1)
    * [zzz](#F2)
...

##First
###F1
###F2
```
##目录
* [First](#First)

##目录
* [横线](#横线)
* [标题](#标题)
* [文本](#文本)
    * 普通文本


.

.

.

.

.

.

.

.

.

.

.

.

.



First
-----------

###F1

###F2

#Second
###S1
###S2


横线
-----------



换行方式除了空一行也可以用`<br>`

测试：
`第一行<br>第二行`

现象：
第一行<br>第二行


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
