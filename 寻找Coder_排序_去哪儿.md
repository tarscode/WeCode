# 寻找Coder

> 刘洋
> 2017.6.7

题目链接：https://www.nowcoder.com/practice/a386fd3a5080435dad3252bac76950a7?tpId=49&tqId=29280&tPage=1&rp=1&ru=/ta/2016test&qru=/ta/2016test/question-ranking

## 内容

### 正文

请设计一个高效算法，再给定的字符串数组中，找到包含"Coder"的字符串(不区分大小写)，并将其作为一个新的数组返回。结果字符串的顺序按照"Coder"出现的次数递减排列，若两个串中"Coder"出现的次数相同，则保持他们在原数组中的位置关系。

给定一个字符串数组A和它的大小n，请返回结果数组。保证原数组大小小于等于300,其中每个串的长度小于等于200。同时保证一定存在包含coder的字符串。

### 输入


```
["i am a coder","Coder Coder","Code"],3
```

### 输出

```
["Coder Coder","i am a coder"]
```

## 分析

本题比较复杂的一点是需要考虑对输出结果进行排序,而且要求是稳定的。那么需要自己手写一个冒泡排序。


## 解法

### 方法一

#### 思路

气球颜色数组arr,i从1到n,数组dp[i]表示前i个气球有多少种剪法,map表示某种颜色的气球数目

1. 首先,遍历A中的每一个字符串,计算每一个字符串中包含“coder”的个数,以及包含“coder”字符串数目count
2. 通过num[i]记录A[i]的“coder”个数,index[i]记录num[i]的位置
3. 对num[i]进行排序,同时调整index[i]
4. 输出前index中前count项的字符串

复杂分析

- 时间复杂度O(n2)
- 空间复杂度O(n)

#### 备注

- 冒泡排序从大到小的顺序

#### 代码

```
public class Coder {

    public String[] findCoder(String[] A, int n) {
        int[] num = new int[n]; //记录每个字符串Coder的次数
        char[] targetA = {'c', 'o', 'd', 'e', 'r'};
        char[] targetB = {'C', 'O', 'D', 'E', 'R'};
        int count = 0; //包含“coder”的字符串数目
        for (int i = 0; i < n; i++) {
            int cur = 0; //当前字符串“coder”的数量
            char[] arr = A[i].toCharArray();
            for (int j = 0; j < arr.length - 4; j++) {
                if (arr[j] == targetA[0] || arr[j] == targetB[0]) { //找到'c'或者'C'
                    for (int k = j + 1, l = 1; l <= 4; k++, l++) {
                        if (arr[k] != targetA[l] && arr[k] != targetB[l]) { //匹配“coder”{
                            break;
                        }
                        if (l == 4) {
                            cur++;//包括一个coder
                        }
                    }
                }
            }
            num[i] = cur;//记录当前字符串包含“coder”的个数
            count = cur != 0 ? count + 1 : count;
        }
        int[] index = new int[n];
        sort(num, index);
        String[] res = new String[count];//输出结果
        for (int i = 0; i < count; i++) {
            res[i] = A[index[i]];
        }
        return res;
    }

    //两数组排序
    private static void sort(int[] arr, int[] index) {
        int n = arr.length;
        for (int i = 0; i < n; i++) {
            index[i] = i;
        }

        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (arr[j] < arr[j + 1]) {
                    exch(arr, j, j + 1);
                    exch(index, j, j + 1);
                }
            }
        }
    }

    //交换
    private static void exch(int[] arr, int i, int j) {
        int tempA = arr[i];
        arr[i] = arr[j];
        arr[j] = tempA;
    }

}
```