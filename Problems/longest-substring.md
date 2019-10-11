## 题目

Longest Substring

寻找最长相同子串。



## 题意

与LCS问题不同的是这里的相同子串是要连续的。所以dp\[i]\[j]的状态转移方程在字符不相等时，要从0开始。并且每次字符相等更新dp时要记录最大值。因为dp不是连续的。



## 代码

```java
public class LongestSubstring {
    public static int longest(String s, String t){
        int slen=s.length();
        int tlen=t.length();
        int[][] dp=new int[slen+1][tlen+1];
        for(int i=0;i<slen+1;i++)
            dp[i][0]=0;
        for(int j=0;j<tlen+1;j++)
            dp[0][j]=0;
        int ans=0;
        for(int i=1;i<slen+1;i++){
            for(int j=1;j<tlen+1;j++){
                if(s.charAt(i-1)!=t.charAt(j-1))
                    dp[i][j]=0;
                else{
                    dp[i][j]=dp[i-1][j-1]+1;
                    ans=Math.max(dp[i][j], ans);
                }
            }
        }
        return ans;
    }

    public static void main(String[] args) {
        System.out.println(longest("abd", "acd"));
    }
}

```

