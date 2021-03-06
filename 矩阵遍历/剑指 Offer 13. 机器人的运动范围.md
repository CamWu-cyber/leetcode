# 剑指 Offer 13. 机器人的运动范围
地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

##### 示例1
    输入：m = 2, n = 3, k = 1
    输出：3
    
##### 示例2
    输入：m = 3, n = 1, k = 0
    输出：1
    
思路：DFS。此题同剑指 Offer 12. 矩阵中的路径一样也是用DFS做，但是没有回溯了，改为把访问过的节点放入visited的集合中。

1. i,j为坐标，si,sj为各位的数位之和。

2. 终止条件：越界或者si+sj > k 或者 (i,j)已经被访问过了，返回0

3. 回溯返回：本单元格的可达解总数 = 1+下方可达解总数+右方可达解总数

4. 想象19,20 位数之和差为8，1,2 位数之和差为1，所以两个相邻数之间的数位之和的关系是当b%10 == 0时，sb = sa-8; 当b%10 != 0时，sb = sa+1。**奇技淫巧**

        #!/usr/bin/python
        class Solution:
            def movingCount(self, m: int, n: int, k: int) -> int:
                # DFS
                # i,j坐标，si,sj各位的数位之和
                # 终止条件：越界或者si+sj > k 或者 (i,j)已经被访问过了，返回0
                # 回溯返回：本单元格的可达解总数 = 1+下方可达解总数+右方可达解总数
                # 19,20 位数之和差为8
                # 1,2 位数之和差为1
                # 所以两个相邻数之间的数位之和的关系是当b%10 == 0时，sb = sa-8; 当b%10 != 0时，sb = sa+1 奇技淫巧了~
                def dfs(i, j, si, sj):
                    if i >= m or j >= n or si+sj > k or (i, j) in visited:
                        return 0
                    visited.add((i, j))
                    return 1 + dfs(i+1, j, si+1 if (i+1)%10 else si-8, sj) + dfs(i, j+1, si, sj+1 if (j+1)%10 else sj-8)

                visited = set()
                res = dfs(0, 0, 0, 0)
                return res

        if __name__ == '__main__':
            obj = Solution()
            print(obj.movingCount(2, 3, 1))
  
#### 运行结果
    3
