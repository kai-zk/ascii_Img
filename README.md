Python 图片转字符画
一、实验介绍
本实验用 50 行 Python 代码完成图片转字符画小工具。通过本实验将学习到 Linux 命令行操作，Python 基础，pillow 库的使用，argparse 库的使用。

1.1 实验知识点
本节实验中我们将实践以下知识：

Linux 命令行操作
Python 基础
pillow 库的使用
argparse 库的使用（参考教程）
1.2 实验环境
python3.5
pillow-5.1.0
PIL 是一个 Python 图像处理库，是本课程使用的重要工具，使用下面的命令来安装 pillow（PIL）库：

$ sudo pip3 install pillow


二、实验原理
字符画是一系列字符的组合，我们可以把字符看作是比较大块的像素，一个字符能表现一种颜色（暂且这么理解吧），字符的种类越多，可以表现的颜色也越多，图片也会更有层次感。

问题来了，我们是要转换一张彩色的图片，这么多的颜色，要怎么对应到单色的字符画上去？这里就要介绍灰度值的概念了。

灰度值：指黑白图像中点的颜色深度，范围一般从0到255，白色为255，黑色为0，故黑白图片也称灰度图像

我们可以使用灰度值公式将像素的 RGB 值映射到灰度值：

gray ＝ 0.2126 * r + 0.7152 * g + 0.0722 * b
这样就好办了，我们可以创建一个不重复的字符列表，灰度值小（暗）的用列表开头的符号，灰度值大（亮）的用列表末尾的符号。

三、实验步骤
创建 ascii.py 文件

首先导入必要的库，argparse 库是用来管理命令行参数输入的

from PIL import Image
import argparse
下面是我们的字符画所使用的字符集，一共有 70 个字符，字符的种类与数量可以自己根据字符画的效果反复调试

`ascii_char = list("$@B%8&WM#*oahkbdpqwmZO0QLCJUYXzcvunxrjft/\|()1{}[]?-_+~<>i!lI;:,\"^`'. ")`
下面是RGB值转字符的函数：

```python
def get_char(r,g,b,alpha = 256):
    if alpha == 0:
        return ' '
    length = len(ascii_char)
    gray = int(0.2126 * r + 0.7152 * g + 0.0722 * b)

    unit = (256.0 + 1)/length
    return ascii_char[int(gray/unit)]
```
完整代码见：ascii.py 



ascii_dora.png

最后，使用刚刚编写的 ascii.py 来将下载的 img.png 转换成字符画。

$ python3 ascii.py img.png


注意，不同的环境中显示的效果可能不尽相同

终端显示的字体是不是等宽字体，终端显示的行高和行宽，输入输出的图像宽高等等，这些都会影响显示效果

