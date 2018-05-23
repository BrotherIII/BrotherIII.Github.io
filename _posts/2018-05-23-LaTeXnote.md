---
layout: post
title: LaTeX写公式的几个细节
date: 2018-05-17
categories: blog
tags: [LaTeX]
description: 
---

本科毕业论文写作的时候，虽然也可以用word排版，但是面对公式较多的情形，LaTeX仍然是最优选择。何况LaTeX才有13格不是（笑）。LaTeX写作的时候有一些现成的模板可以套用，公式符号之类的也很容易搜索到，
但是公式输入时候有的细节容易被忽略。所以我在这里记录一下。


# 一、单行公式编号
单行公式在equation环境下输入后会有自动编号。
 '''
\begin{equation}
\label{equ:1}
a^2 + b^2 = c^2
\end{equation}
 '''
当需要引用的时候，在文中使用(\req{equ:1})，编译之后就能自动引用该公式的编号了，这种方式避免了手动编号可能的错误，编号变动了也很容易修改，推荐使用。另外，中文论文需要编译两次才能正确显示序号。  

对于不需要编号的单行公式，可以直接这样输入
 '''
$$ a^2 + b^2 = c^2 $$
 ''' 

# 二、连等式编号
连等式，或者一组多个等式，通常在eqnarray或者align环境下输入。但是eqnarray在实际使用的时候由于这样那样的一些问题，表现有时候会不及align。
如果公式不需要编号，可以在“$$ $$”之中嵌入aligned环境输入
 '''
$$\begin{aligned}
f(x)&= (x+a)(x+b)\\
&= x^2+(a+b)x+ab
\end{aligned}$$
 '''
“&”表示对齐点，“\\”表示换行。或者可以在align*环境下输入。
 '''
\begin{align*}
f(x)&= (x+a)(x+b)\\
&= x^2+(a+b)x+ab
\end{align*}
 '''
类似的，如果一行内容很长，需要截断，应该这么输入
 '''
$$\begin{aligned}
f(x)&= (x+a)(x+b)+(x+b)(x+c)\\
&\quad +(x+c)(x+a)
&= x^2+(a+b)x+ab
\end{aligned}$$
 '''
“\quad”表示空一格，因为加号不应该和等号对齐，而是在后面一格的位置。
如果公式需要编号，可以把aligned环境嵌入到equation环境中
 '''
\begin{equation}
\label{equ:2}
\begin{aligned}
f(x)&= (x+a)(x+b)\\
&= x^2+(a+b)x+ab
\end{aligned}
\end{equation}
 '''
这样输出的公式是有唯一一个编号的，并且这个编号是居中显示的。  

如果需要编号在最后一行显示，可以使用align环境
 '''
\begin{align}
f(x)&= (x+a)(x+b)\nonumber \\
&= x^2+(a+b)x+ab\label{equ:2}
\end{align}
 '''
这样输出的公式编号就在最后一行了，并且仍然可以进行自动引用。“\nonumber”表示那一行没有编号，因为align环境默认是每行都有编号的。

# 三、函数名
LaTeX输入函数名通常需要加一个反斜杠，比如'''\sin(x)'''。对于没有直接定义的函数，比如argmin，如果输入
 '''
$$ argmin f(x) $$
 '''
会发现前面的argmin是斜体，这是由于argmin被当做了一个变量而不是函数名。如何用正体显示呢？一种方式是在导言区加上
 '''
\DeclareMathOperator*{\argmin}{argmin}
 '''
这样就可以像引用正弦函数“sin”一样使用argmin。但如果论文中这个函数只出现一遍，这样做就显得不经济了。这时候可以采取另一种方式
 '''
$$ {\rm argmin} f(x) $$
 '''
这样可以直接将argmin转换成正体。





