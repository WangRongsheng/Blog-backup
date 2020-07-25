---
title: The Game of Life
date: 2019-09-18 22:47:02
thumbnail: https://i.loli.net/2019/09/18/ctX48F3p1rhdyfI.png
tags: 生命游戏
categories: Python
---
#引言

Python 的 Matplotlib 是最常用的图表绘制以及数据可视化库。我们对折线图、柱状图以及热力图都比较熟悉，但你知道用 Matplotlib 还能做简单的动画吗？

<!--more-->

下面就是用 Matplotlib 制作动画的例子。展示的是 John Conway 的 《The Game of Life》，这是一个 Metis（数据科学夏令营）中的编程挑战题目，同时给了我一个机会让我知道Matpltlib可以制作动图。看看结果的动图：

<a href="https://sm.ms/image/CAmo9P5xGeOHMcR" target="_blank"><img src="https://i.loli.net/2019/09/18/CAmo9P5xGeOHMcR.gif" ></a>

这篇文章的重点还是主要放在 python 中如何用 Matploylib 制作动画。

但如果你不太熟悉模拟游戏的话（它更像是可以看的模拟动画，而非可以玩的游戏），我来给大家介绍一下规则：

1. 一开始先设置一个 N×N 的网格（我的动画中用的是 50×50 ）；

2. 接着随机地向格子中填充“小细胞”（一开始随机地从 2500 个格子中选取 1500 个进行填充）；

3. 如果邻居小细胞少于等于 1 个，那格子中的小细胞会死掉；

4. 如果邻居大于等于 4 个的也会死掉；

5. 只有 2 个或 3 个邻居时可以生存；

6. 空的格子中如果正好有 3 个邻居，则会长出 1 个新的“小细胞”；

通过对规则的阅读我最先想到的是：[生命游戏](https://baike.sogou.com/v9062794.htm?fromTitle=生命游戏)

# 代码实现

**注意:**我运行采用的是**Anaconda3集成环境**；程序运行**两次**，第一次营造运行环境，第二次运行程序输出。

```python
import time
from IPython import display
import matplotlib.pyplot as plt
import matplotlib.animation as animation

import numpy as np
import seaborn as sns
import random

# Some helper functions

# Initialize the board with starting positions
def init_board(pos_list, my_board):
    for pos in pos_list:
        my_board[pos[0], pos[1]] = 1
    return my_board

# Make sure padded border values are always zero
def force_pad_zero(my_board):
    edge_row_0 = 0
    edge_row_1 = my_board.shape[0] - 1
    edge_col_0 = 0
    edge_col_1 = my_board.shape[1] - 1
    for index, row in enumerate(my_board):
        if index == 0:
            row[:] = 0
        elif index == edge_row_1:
            row[:] = 0
        else:
            row[edge_col_0] = 0
            row[edge_col_1] = 0
    for col in my_board:
        col[edge_row_0] = 0
        col[edge_row_1] = 0
    return my_board

# Figure out the number of neighbors for a given cell
def calc_neighbors(row, col, my_board):
    b = force_pad_zero(my_board)
    num_neighbors = (b[row-1,col-1] + b[row+0,col-1] + b[row+1,col-1] + b[row+1,col+0] 
                   + b[row+1,col+1] + b[row+0,col+1] + b[row-1,col+1] + b[row-1,col+0])
    return num_neighbors

# Update the board based on the game rules, each call to update_board is one turn
def update_board(my_board):
    old_board = my_board.copy()
    set_zero = []
    set_one = []
    # Loop through board and update according to rules
    for i, row in enumerate(my_board[1:-1,1:-1]):
        for j, col in enumerate(row):
            true_i = i + 1
            true_j = j + 1
            # Update based on number of neighbors (using calc_neighbors)
            # set_zero and set_one are lists that tell me the coordinates of cells that require updating
            if (((calc_neighbors(true_i, true_j, my_board) <= 1) 
                  or (calc_neighbors(true_i, true_j, my_board) >= 4))
                  and my_board[true_i, true_j] != 0):
                set_zero.append([true_i, true_j])
            elif ((calc_neighbors(true_i, true_j, my_board) == 3)
                  and my_board[true_i, true_j] == 0):
                set_one.append([true_i, true_j])
    # Update the required cells
    for index, val in enumerate(set_zero):
        my_board[val[0], val[1]] = 0
    for index, val in enumerate(set_one):
        my_board[val[0], val[1]] = 1
    return my_board

# Input variables for the board
boardsize = 50        # board will be X by X where X = boardsize
pad = 2               # padded border, do not change this!
initial_cells = 1500  # this number of initial cells will be placed 
                      # in randomly generated positions

# Get a list of random coordinates so that we can initialize 
# board with randomly placed organisms
pos_list = []
for i in range(initial_cells):
    pos_list.append([random.randint(1, boardsize), 
                     random.randint(1, boardsize)])

# Initialize the board
my_board = np.zeros((boardsize+pad, boardsize+pad))
my_board = init_board(pos_list, my_board)

##### Animate the board #####
# This will throw an error the first time you run the code, but the program will run properly if you
# execute the cell again (there is an error with the animation package that I cannot seem to get rid of)

# Required line for plotting the animation
%matplotlib notebook
# Initialize the plot of the board that will be used for animation
fig = plt.gcf()
# Show first image - which is the initial board
im = plt.imshow(my_board)
plt.show()
plt.savefig(fname='game_of_life', dpi=150)

# Helper function that updates the board and returns a new image of
# the updated board animate is the function that FuncAnimation calls
def animate(frame):
    im.set_data(update_board(my_board))
    return im,

# This line creates the animation
anim = animation.FuncAnimation(fig, animate, frames=200, 
                               interval=50)
```

# 总结

希望这篇文章能帮到大家。在结束之前，让我来帮助大家脑补更多我们今天学到的动画功能在数据科学上的应用：

- 一个个地画出蒙特卡洛模拟数据，你能观察到最终的分布是如何逐步形成的；

- 按顺序遍历时间序列数据，可以描绘你的模型或数据在新的观察角度下有什么表现；

- 当你改变输入参数时，比如族群数，可以展现你的算法是如何划分族群的；

- 根据时间或不同的数据子集生成关联热力图，用于观察不同的样本是如何影响你的模型的预期参数的。