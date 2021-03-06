# 剑指 Offer 15. 二进制中1的个数
请实现一个函数，输入一个整数（以二进制串形式），输出该数二进制表示中 1 的个数。例如，把 9 表示成二进制是 1001，有 2 位是 1。因此，如果输入 9，则该函数输出 2。

#### 示例1
    输入：11
    输出：3
    解释：输入11的二进制串 1011 中，共有三位为 '1'。

#### 示例2
    输入：128
    输出：1
    解释：输入128的二进制串 10000000 中，共有一位为 '1'。
    
思路：这里用一个trick， 可以轻松求出。 就是n & (n - 1) 可以消除 n 最后的一个1的原理。这样我们可以不断进行n = n & (n - 1)直到n === 0 ， 说明没有一个1了。这个时候我们消除了多少1变成一个1都没有了， 就说明n有多少个1了。

    #!/usr/bin/python
    class Solution:
        def hammingWeight(self, n: int) -> int:
            # 这里用一个trick， 可以轻松求出。 就是n & (n - 1) 可以消除 n 最后的一个1的原理。
            # 这样我们可以不断进行n = n & (n - 1)直到n === 0 ， 说明没有一个1了。
            # 这个时候我们消除了多少1变成一个1都没有了， 就说明n有多少个1了。
            res = 0
            while n:
                n &= n-1
                res += 1
            return res

    if __name__ == '__main__':
      obj = Solution()
      print(obj.hammingWeight(3))
      print(obj.hammingWeight(128))

#### 运行结果
    2
    1
