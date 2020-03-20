---
title: python生成迷宫
date: 2019-10-14 20:54:32
thumbnail: https://i.loli.net/2019/10/14/76235bmHWNExioq.png
tags: 迷宫
categories: Python
---

算法简介:

1. 生成一张网格，把网格里面的所有边都存进一个列表edgeList里面.

2. 从(0, 0)开始，做DFS。每次DFS的时候，随机地选择四周一个没有走过的格子，凿墙过去，把道路打通。凿墙的时候，把edgeList列表中相对应的那堵墙删除掉。

3. 将剩下的没有凿开过的墙画出来，就是一个完整的迷宫了。

<!--more-->

```python
import sys
import matplotlib.pyplot as plt
from random import randint

WIDTH  = 60
HEIGHT = 40
sys.setrecursionlimit(WIDTH * HEIGHT)

def initVisitedList():
	visited = []
	for y in range(HEIGHT):
		line = []
		for x in range(WIDTH):
			line.append(False)
		visited.append(line)
	return visited

def drawLine(x1, y1, x2, y2):
	plt.plot([x1, x2], [y1, y2], color="black")

def removeLine(x1, y1, x2, y2):
	plt.plot([x1, x2], [y1, y2], color="white")

def get_edges(x, y):
	result = []
	result.append((x, y, x, y+1))
	result.append((x+1, y, x+1, y+1))
	result.append((x, y, x+1, y))
	result.append((x, y+1, x+1, y+1))

	return result

def drawCell(x, y):
	edges = get_edges(x, y)
	for item in edges:
		drawLine(item[0], item[1], item[2], item[3])

def getCommonEdge(cell1_x, cell1_y, cell2_x, cell2_y):
	edges1 = get_edges(cell1_x, cell1_y)
	edges2 = set(get_edges(cell2_x, cell2_y))
	for edge in edges1:
		if edge in edges2:
			return edge
	return None

def initEdgeList():
	edges = set()
	for x in range(WIDTH):
		for y in range(HEIGHT):
			cellEdges = get_edges(x, y)
			for edge in cellEdges:
				edges.add(edge)
	return edges

def isValidPosition(x, y):
	if x < 0 or x >= WIDTH:
		return False
	elif y < 0 or y >= HEIGHT:
		return False
	else:
		return True

def shuffle(dX, dY):
	for t in range(4):
		i = randint(0, 3)
		j = randint(0, 3)
		dX[i], dX[j] = dX[j], dX[i]
		dY[i], dY[j] = dY[j], dY[i]

def DFS(X, Y, edgeList, visited):
	dX = [0,  0, -1, 1]
	dY = [-1, 1, 0,  0]
	shuffle(dX, dY)
	for i in range(len(dX)):
		nextX = X + dX[i]
		nextY = Y + dY[i]
		if isValidPosition(nextX, nextY):
			if not visited[nextY][nextX]:
				visited[nextY][nextX] = True
				commonEdge = getCommonEdge(X, Y, nextX, nextY)
				if commonEdge in edgeList:
					edgeList.remove(commonEdge)
				DFS(nextX, nextY, edgeList, visited)

plt.axis('equal')
plt.title('Maze')
edgeList = initEdgeList()
visited  = initVisitedList()
DFS(0, 0, edgeList, visited)
edgeList.remove((0, 0, 0, 1))
edgeList.remove((WIDTH, HEIGHT-1, WIDTH, HEIGHT))
for edge in edgeList:
	drawLine(edge[0], edge[1], edge[2], edge[3])
plt.show()
```