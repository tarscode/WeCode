# 风口上的猪

> 刘洋
> 2017.5.31

题目链接：https://www.nowcoder.com/practice/9370d298b8894f48b523931d40a9a4aa?tpId=49&tqId=29233&tPage=1&rp=1&ru=%2Fta%2F2016test&qru=%2Fta%2F2016test%2Fquestion-ranking

## 内容

### 正文


风口之下，猪都能飞。当今中国股市牛市，真可谓“错过等七年”。 给你一个回顾历史的机会，已知一支股票连续n天的价格走势，以长度为n的整数数组表示，数组中第i个元素（prices[i]）代表该股票第i天的股价。 假设你一开始没有股票，但有至多两次买入1股而后卖出1股的机会，并且买入前一定要先保证手上没有股票。若两次交易机会都放弃，收益为0。 设计算法，计算你能获得的最大收益。 输入数值范围：2<=n<=100,0<=prices[i]<=100 

### 输入


```
3,8,5,1,7,8
```

### 输出


```
12
```

## 分析

题目与LeetCode中的Best Time to Buy and Sell Stock III相同

## 解法

### 第一种:记忆搜索法

#### 思路

1. 从左向右遍历，记录前i次交易的最大收益left[i]
2. 从右向左遍历，记录后j次交易的最大所以right[j]
3. 在次遍历，获取最大的left[i]+right[i]

复杂分析

- 时间复杂度O(n)
- 空间复杂度O(n)

#### 备注

- 考虑三种情况:(1)交易1次(2)交易2次(3)交易0次

#### 代码


```
public class Solution {

    /**
     * 计算你能获得的最大收益
     *
     * @param prices Prices[i]即第i天的股价
     * @return 整型
     */
    public int calculateMax(int[] prices) {
        int n = prices.length;
        int res = 0; //记录收益结果的最大值
        int min = prices[0]; //记录价格的最小值
        int[] left = new int[n];
        int[] right = new int[n];
        //从左向右遍历,记录前i天的最大收益
        for (int i = 0; i < n; i++) {
            int cur = prices[i] - min; //第i天收益
            res = Math.max(res, cur);
            left[i] = res;
            min = Math.min(prices[i], min); //更新价格最小值
        }
        int max = prices[n - 1];
        res = 0; //清空变量
        //从右向左遍历,记录后i天的最大收益
        for (int i = n - 1; i >= 0; i--) {
            int cur = max - prices[i]; //第i天收益
            res = Math.max(cur, res);
            right[i] = res;
            max = Math.max(max, prices[i]); //更新价格最大值
        }
        for (int i = 0; i < n; i++) {
            int cur = left[i] + right[i];
            res = Math.max(res, cur);
        }
        return res;
    }

    public static void main(String[] args) {
        Solution t = new Solution();
        int[] arr = {3, 8, 5, 1, 7, 8};
        System.out.println(t.calculateMax(arr));
    }
}
```
