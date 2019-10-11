## 题目

最长公共子序列Longest Common Sequence

找出两个字符串中最长公共子序列并返回长度。



## 思考过程

首先是典型的动态规划问题。那从小问题思考如何把问题分割成更小的问题。

假设两个字符串为"acd", "abd"。从最后一个字符开始比较。

1. 'd'相等。所以ans+1.问题变成了找1+lcs("ac", "ab")
2. 'c'不等于'b'。此时分割方法是分别去掉当前字符串最后一个字符来比较。即变成找1+max(lcs("ac","a")), lcs("a","ab")).
3. 'c'不等于'a', 'a不等于'b'。继续分割。即1+max( max(lcs("a","a"), lcs("ac","")),  max( lcs("","ab"), lcs("a","a")) ).
4. 当其中有一个字符串长度为0即为“”时，最长公共子序列长度必然为0. 然后各剩一个的情况的子情况也是有一个子串为""就不再写出来。所以已经分解得到最小的问题了。即1+max( 1, 1)=2
5. 答案为2

以上问题可以看出最小问题是有其中一个字符串为""。



然后是dp表。下表是初始情况。虽然上面是从后往前，但动态规划是从小问题推广到大问题。即dp[i]=op(dp[i-1])。op为某种操作。所以从上面得知，最小问题时长度为0，即初始情况。这里dp\[i]\[j]表示s.substring(0,i)与t.substring(0, j)的最长公共子序列长度。因为最小问题是其中一个长度为0，即dp\[0]\[j]或者dp\[i]\[0].所以dp的长度分别为s.length()+1, t.length()+1。



|      |   "" |  a   | b    | d    |
| :--- | ---: | :--: | ---- | ---- |
| ""   |    0 |  0   | 0    | 0    |
| a    |    0 |      |      |      |
| b    |    0 |      |      |      |
| d    |    0 |      |      |      |



然后就是状态转移方程。分成两种。
$$
dp[i][j]=dp[i-1][j-1]+1, s[i]==t[j]时
$$

$$
dp[i][j]=Max(dp[i-1][j], dp[i][j-1]), s[i]!=t[j]时
$$
行，列一次填写，dp\[slen]\[tlen]即最后答案



## 代码

```java
public class LCS {
    public int lcs(String t, String s){
        int tlen=t.length();
        int slen=s.length();
        int[][] dp=new int[tlen+1][slen+1];
        for(int i=0;i<tlen+1;i++){
            dp[i][0]=0;
        }
        for(int j=0;j<slen+1;j++){
            dp[0][j]=0;
        }
        for(int i=1;i<tlen+1;i++){
            for(int j=1;j<slen+1;j++){
                if(t.charAt(i-1)==s.charAt(j-1))
                    dp[i][j]=dp[i-1][j-1]+1;
                else
                    dp[i][j]=Math.max(dp[i-1][j], dp[i][j-1]);
            }
        }
        return dp[tlen][slen];
    }
}

```





