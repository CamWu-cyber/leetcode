# AUC
首先要明白ＡＵＣ的物理含义不仅是ＲＯＣ曲线下的面积，ＡＵＣ还有另外一个物理含义就是：给定正样本Ｍ个，负样本Ｎ个，以及他们的预测概率（０－１）之间，那么ＡＵＣ的含义就是所有穷举所有的正负样本对，如果正样本的预测概率大于负样本的预测概率，那么就＋１；如果如果正样本的预测概率等于负样本的预测概率，那么就＋0.5,　如果正样本的预测概率小于负样本的预测概率，那么就＋０；最后把统计处理的个数除以Ｍ×Ｎ就得到我们的ＡＵＣ.

    def AUC(label, pre):
      """
      适用于ｐｙｔｈｏｎ3.0以上版本
       """
      #计算正样本和负样本的索引，以便索引出之后的概率值
        pos = [i for i in range(len(label)) if label[i] == 1]
        neg = [i for i in range(len(label)) if label[i] == 0]

        auc = 0
        for i in pos:
            for j in neg:
                if pre[i] > pre[j]:
                    auc += 1
                elif pre[i] == pre[j]:
                    auc += 0.5

        return auc / (len(pos)*len(neg))


    if __name__ == '__main__':
        label = [1,0,0,0,1,0,1,0]
        pre = [0.9, 0.8, 0.3, 0.1, 0.4, 0.9, 0.66, 0.7]
        print(AUC(label, pre))

##### 运行结果
    0.5666666666666667
