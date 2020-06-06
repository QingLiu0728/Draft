

**There is no [TOC] program in vs code**


# Simple usage of Markdown and test in VS code

# This is a title
## This is a smaller title

> This is a block

<!-- [Google home url](www.google.com) -->



<center> This is how to make line align center
***

<font color='yellow'>字体颜色</font><br>
<font face="微软雅黑" color="red" size="6">字体及字体颜色和大小</font>

---

~~This a line that has been stroken through~~ <br>
<u>This is how to make a underline</u>


```

```
Head
Column A | Column B | Column C
---------|:----------:|---------:
 A1 | B1 | C1
 A2 | B2 | C2
 A3 | B3 | C3


<!-- ![](https://cn.bing.com/images/search?view=detailV2&ccid=rlDdWkzL&id=3275826ED23BEAB7545328F349126D62ED75D595&thid=OIP.rlDdWkzLHZJcR0a8cLfS7gHaLH&mediaurl=http%3a%2f%2fphotocdn.sohu.com%2f20120704%2fImg347293712.jpg&exph=750&expw=500&q=%E4%B8%87%E8%8C%9C&simid=607988739533898843&selectedIndex=2&ajaxhist=0) -->

This is <br> **how to shift to another line**


<detail>
<summary></summary>
</detail>

## LaTex with Markdown
### Matrix
<!-- Use matrix with typical usage -->
1. standard matrix
    $
    \begin{matrix}
    1 & 2 & 3 \\
    4 & 5 & 6 \\
    7 & 8 & 9
   \end{matrix}
    $

2. 使用**\$\begin{matrix}1 & 2& 3 \\ 4 & 5 & 6\end{matrix}\$**来生成矩阵，矩阵命令中每一行以 \\\ 结束，矩阵的元素之间用**&**来分隔开。

3. 
$$
\left[
      \begin{array}{cc|c}
        1 & 2 & 3 \\
        4 & 5 & 6
      \end{array}
    \right]
$$

$$
\begin{gathered}
\begin{matrix} 0 & 1 \\ 1 & 0 \end{matrix}
\quad
\begin{pmatrix} 0 & -i \\ i & 0 \end{pmatrix}
\quad
\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}
\quad
\begin{Bmatrix} 1 & 0 \\ 0 & -1 \end{Bmatrix}
\quad
\begin{vmatrix} a & b \\ c & d \end{vmatrix}
\quad
\begin{Vmatrix} i & 0 \\ 0 & -i \end{Vmatrix}
\end{gathered}
$$

### Integration
$\int_0^1 x^2 {\rm d}x$

