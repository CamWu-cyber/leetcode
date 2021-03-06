# 剑指 Offer 17. 打印从1到最大的n位数
输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

#### 示例1
    输入: n = 1
    输出: [1,2,3,4,5,6,7,8,9]
    
思路：回溯法框架。每一位上面都是0-9，个位、十位、百位...依次组合。path的初始值是空字符串，往后叠加即可。

    #!/usr/bin/python
    class Solution:
      def printNumbers(self, n):
        def backtrack(path, start):
          if start == n:
            res.append(int(path))
            return None
          for i in range(10):
            # 先转成str方便叠加，后面res中再转成int
            path += str(i)
            backtrack(path, start+1)
            path = path[:-1]
        path = ''
        res = []
        backtrack(path, 0)
        # 题目要求从1开始，所以不要0
        return res[1:]

    if __name__ == '__main__':
      obj = Solution()
      print(obj.printNumbers(2))
      
#### 运行结果
    [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99]
