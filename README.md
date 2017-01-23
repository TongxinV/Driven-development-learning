GitHub上的markdown格式一些利于排版的用法
=======================================
> 想全面了解的可以参考[果冻虾仁的文章](https://github.com/guodongxiaren/README)，欢迎补充谈论


##目录
* [目录的实现](#目录的实现)
* [文字换行](#文字换行)
* [程序结构样式写法](#程序结构样式写法)
* [添加文本框的效果](#添加文本框的效果)
* [前面空四个空格](#前面空四个空格)
* [流程图变横向](#流程图变横向)







## 目录的实现
GitHub上不支持[TOC]

想要目录可以这样实现

```
##目录
* [中文](#中文)    //标题要是中文才可以不知道为什么，试了英文不行
    * [中文a](#中文a)
    * [中文b](#中文b)
...
##中文
###中文a
###中文b
```


## 文字换行

换行方式除了空一行也可以用`<br>`

测试：
`第一行<br>第二行`

现象：
第一行<br>第二行


## 程序结构样式写法

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



## 添加文本框的效果

文本框的结构：

    ┌──────────────────────────┐
    │       TEXT               │ 
    │       TEXT               │
    └──────────────────────────┘    





## 前面空四个空格

    前面空四个空格有类似于代码片段的效果
        
## 流程图变横向

> 添加right或者left

```
op1=>operation: My Ope
op2=>operation: My Ope
op3=>operation: My Ope

op1(right)->op2(right)->op3

```


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
