---
layout:     post
title:      "岛屿周长"
subtitle:   " \"Hello World, Hello Blog\""
date:       2018-04-01 15:48:00
author:     "suny"
catalog: true
categories: Leetcode
tags:
    - 笔记
---
<img src="/img/IslandPerimeter.jpg"/>

python代码
	
    class Solution(object):
    def islandPerimeter(self, grid):
        count = 0
        def is_water(i, j):
			#是水和超出想x,y边界都返回True
            return i<0 or j<0 or i>len(grid)-1 or j>len(grid[i])-1 or grid[i][j]==0
        #每个单元的四周坐标，原点设为0
		bound = ((0,1),(0,-1),(1,0),(-1,0))
        for (i,row) in enumerate(grid):
            for (j,colum) in enumerate(grid[i]):
                if colum == 1:
                    for pos in bound:
                        if is_water(i+pos[0], j+pos[1]):
                            count+=1
        return count        

        
	s = Solution()
	a = s.islandPerimeter([[1],[0]])
	print(a)

	
	


