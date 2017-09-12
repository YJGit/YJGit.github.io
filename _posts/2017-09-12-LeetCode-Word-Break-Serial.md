---
layout: post
title:  LeetCode之Word Break(I/II)题解
date:   2017-09-12 23:11:00 +0800
categories: 算法学习
tag: LeetCode
---

* content
{:toc}

## 题目一 Word Break    

**题目描述:** 见[https://leetcode.com/problems/word-break/description/](https://leetcode.com/problems/word-break/description/)  
**大意:** 给定一个非空字符串s和一个非空的由一些单词组成的字典wordDict，判定s是否能够被分割成由wordDict中的单词组成，可以认为wordDict中单词不重复。    
**待实现函数：**  

    
	class Solution {  
	public:  
	    bool wordBreak(string s, vector<string>& wordDict) {
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;这道题的一个比较好的解法是用动态规划。即采用一个变量，这里用```vector<int> res```记录从s的长度1到整个长度的字串是否能被wordDict表示，也就是说res[i]=1表示s的0到i长度的字串能够被wordDict表示，res[i]=0则不可以，特殊情况是res[0]=1。递推式是res[i]=1 (res[j]=1 对于某个j,0=<j<i),否则res[i]=0，然后从1遍历到len(s的长度)即可。 

**解题源码：**  

	class Solution {
	public:
	    bool wordBreak(string s, vector<string>& wordDict) {
	        int len = s.length();
	        vector<int> res(len + 1, 0);  //res[i]记录0到i长度的字串能不能被wordDict表示
	        res[0] = 1;
	        for(int i = 1; i <= len; i++){
	            for(int j = 0; j < i; j++){  //遍历所有可能的组合
	                if(res[j]) {
	                    string str = s.substr(j, i - j);
	                    if(find(wordDict.begin(), wordDict.end(), str) != wordDict.end()){
	                        res[i] = 1;  //只要判定可以，即可断掉循环
	                        break;
	                    }
	                }
	            }
	        }
	        
	        return res[len];
	    }
	};

## 题目二 Word Break II  

**题目描述:** 见[https://leetcode.com/problems/word-break-ii/description/](https://leetcode.com/problems/word-break-ii/description/)  
**大意:** 给定一个非空字符串s和一个非空的由一些单词组成的字典wordDict，给s以空格断句，分割成wordDict中的单词组成的句子，输出所有可能的组合。     
**待实现函数：**  

    
	class Solution {  
	public:  
	    vector<string> wordBreak(string s, vector<string>& wordDict) {
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;这里很容易想到的是采用递归的方法，不断的处理子串。即遍历s的长度，判断当前的字串在不在wordDict里，在的话，递归处理剩下的字串。但是这样会超时，然后解决方法是采用一个```map<string, vector<string> > m_str_res```的变量记录下中间结果，即某个计算过的字串可以分割成哪些由wordDict中的单词组成的句子，这样就避免了重复计算，详见下面的源码。  

**解题源码：**  

	class Solution {
		map<string, vector<string> > m_str_res;
	public:
	    vector<string> wordBreak(string s, vector<string>& wordDict) {
	        if(m_str_res.find(s) != m_str_res.end()) return m_str_res[s];  //之前有记录，直接返回
	        int len = s.length();
	        vector<string> res;
	        
	        for(int i = 0; i < len; i++){
	            string word = s.substr(0, i + 1);  //要查找的单词
	            string left = s.substr(i + 1);  //剩下的单词
	            if(find(wordDict.begin(), wordDict.end(), word) != wordDict.end()){
	                if(left == "") res.push_back(word);  //剩下单词为""，则直接将此次word加入结果
	                else{
	                    vector<string> _res = wordBreak(left, wordDict);  //_res为剩下单词的处理结果
	                    for(int i = 0; i < _res.size(); i++){
	                        res.push_back(word + " " + _res[i]);  //将word与剩下单词的结果进行组合
	                    }
	                }
	                
	            }
	        }
	        
	        m_str_res[s] = res;  //记录下当前的结果
	        return res;
	    }
	};