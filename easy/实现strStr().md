[TOC]

# 题目描述

实现 [strStr()](https://baike.baidu.com/item/strstr/811469) 函数。

给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)。如果不存在，则返回  **-1**。

**示例 1:**

```
输入: haystack = "hello", needle = "ll"
输出: 2
```

**示例 2:**

```
输入: haystack = "aaaaa", needle = "bba"
输出: -1
```

**说明:**

当 `needle` 是空字符串时，我们应当返回什么值呢？这是一个在面试中很好的问题。

对于本题而言，当 `needle` 是空字符串时我们应当返回 0 。这与C语言的 [strstr()](https://baike.baidu.com/item/strstr/811469) 以及 Java的 [indexOf()](https://docs.oracle.com/javase/7/docs/api/java/lang/String.html#indexOf(java.lang.String)) 定义相符。

# 我的答案

##1、使用equals方法

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack==null||needle==null||haystack.length()<needle.length()){
            return -1;
        }
        if(needle.equals("")||haystack.equals(needle)){
            return 0;
        }
        int i = -1;
        int index = 0;
        String temp = null;
        while(index+needle.length()<=haystack.length()){
            temp = haystack.substring(index,index+needle.length());
            if(temp.equals(needle)){
                i = index;
                return i;
            }
            index++;
        }
        
        return i;
    }
}
```

## 2、转成char[]

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(haystack==null||needle==null||haystack.length()<needle.length()){
            return -1;
        }
        if(needle.equals("")||haystack.equals(needle)){
            return 0;
        }
        int i = -1;
        int index = 0;
        int j = 0;
        int temp = 0;
        char[] hChar = haystack.toCharArray();
        char[] nChar = needle.toCharArray();
        while(index<hChar.length && j<nChar.length){
            if(hChar[index] == nChar[j]){
                if(i==-1&&j==nChar.length-1){
                    i = temp;
                }
                j++;
                index++;
            }else{
                j = 0;
                index = ++temp;
                i=-1;
            }
        }
        
        return i;
    }
}
```

# 官方题解

暂无

# 优秀题解

```java
class Solution {
    public int strStr(String haystack, String needle) {
        if(needle.length()==0)
            return 0;
        
        int i=0;
        int j=0;;
        
            while(i<haystack.length() && j<needle.length())
            {
                if(haystack.charAt(i)==needle.charAt(j))
                {
                    i++;
                    j++;
                }
                else
                {
                    i=i-j+1;
                    j=0;
                }
            }
            if(j==needle.length())
                return i-j;
        else
            return -1;
        
```

# 总结

我的第二种方式和优秀答案差不多，但是人家的更简洁！运用了charAt方式，避免了转char[]。自己对java API的理解还不到位。