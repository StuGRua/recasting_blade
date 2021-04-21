- LC5. 最长回文子串
    - 请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。
- 基本分析ababa：
  - b->aba 或者 a->bab->ababa，由较短子串向长子串递推
  - 单字符子串时必为回文
  - 双字符时看临近字符，dp[i][j]=(s[i]==s[j]) 
  - 多字符时，递推式应该考察上一个子串的情况，以及当前子串开头结尾，递推式dp[i][j]=(dp[i+1][j-1] and s[i]==s[j])
```python
class Solution:
    def longestPalindrome(self, s: str) -> str:
        n=len(s)
        dp = [[False] *n for _ in range(n)] # 注意每个一维列表要单独初始化（引用问题）
        index1,index2=0,0
        for leng in range(n): # 子串长度
            for i in range(n): # 子串开始位置
                j=i+leng # 子串结束位置
                if j>n-1:
                    break
                if leng==0:
                    dp[i][j]=True # 子串为单字符
                elif leng==1:
                    dp[i][j]=(s[i]==s[j]) # 子串为双字符
                else:
                    dp[i][j]=(dp[i+1][j-1] and s[i]==s[j]) # 其他情况的子串
                if dp[i][j] and index2-index1-1<leng+1:
                    index1,index2=i,j+1
        return s[index1:index2]

```