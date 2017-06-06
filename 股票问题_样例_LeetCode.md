# 股票问题

> 刘洋
> 2017.5.31

题目链接：https://leetcode.com/problems/lru-cache/#/description

## 内容

### 正文

给定一个整型数组,第i个元素代表第i天股票的价格,如果只允许你最多完成一次交易,即买一个股票然后再卖一次股票,设计一个算法求得交易的最大值。

### 输入


```
[7, 1, 5, 3, 6, 4]
```

### 输出


```
5
```

## 分析

本质上求出有序数组中两个最大的差值，即后面元素减去前面元素的最大值


## 解法

### 方法一:暴力法

#### 思路

1. 遍历数组prices
2. 求出每一个元素prices[i]作为最小值的情况下，获得的收益最大值

复杂分析

- 时间复杂度O(n2)
- 空间复杂度O(1)

#### 备注

- 注意max变量用long，否则值溢出

#### 代码


```
public int maxProfit(int[] prices) {
        int max = 0;
        for(int i=0;i<prices.length;i++){
            for(int j=i;j<prices.length;j++){
                int profit = prices[j] - prices[i];
                max = profit>max?profit:max;
            }
        }
        return max;
    }
```