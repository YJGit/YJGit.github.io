---
layout: post
title:  LeetCode之Combination Sum(I/II/III/IV)题解
date:   2017-09-09 16:26:00 +0800
categories: 算法学习
tag: LeetCode
---

* content
{:toc}


## 前言

本来不打算写关于LeetCode的题解博客，但是随着刷题的继续，我发现LeetCode的题目很是经典，也很有系统性，比如我今天要写的Combination Sum问题，就包含了I，II，III，IV四道，也许今后还会出现更多，所以我想将这样的题目整理在一起，不仅对于自己算法解题能力有提高，甚至在于自己思考的方式上面也有很大的帮助，故开始做一些题解记录。

## 题目一 Combination Sum  

**题目描述:** 见[https://leetcode.com/problems/combination-sum/description/](https://leetcode.com/problems/combination-sum/description/)  
**大意:** 给一个没有重复数的集合C和一个目标数T，从C中找出所有独特的组合，使他们的和等于T。其中C中的每个数在每次组合中可以随意使用很多次。  
**一些条件:** 所有的数为正整数，最后的答案的集合不能重复。  
**待实现函数：**  

    
	class Solution {  
	public:  
	    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {  
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;很容易想出的一个思路就是利用递归的方法，用一个变量tmp记录当前记录的集合，一个变量ind记录当前查找candidates的下标起始位置，```target == 0```为递归终止条件，此时将tmp记录进答案。  
&nbsp;&nbsp;&nbsp;&nbsp;为了避免答案的重复，并且利于判断，可将candidates先进行排序，那么在每个非终止的递归函数体里，即可循环查找下标从ind开始(包括ind)的candidates数，当满足```candidates[i] < target``，即可进行下一轮递归查找。  
**解题源码：**  

	class Solution {
	public:
	    vector<vector<int> > combinationSum(vector<int> &candidates, int target) {
	        sort(candidates.begin(), candidates.end());
	        vector<vector<int> > res;  //最终的结果
	        vector<int> tmp;  //递归查找过程中记录的集合
	        helper(candidates, target, res, tmp, 0);  //0表示从下标0开始
	        return res;
	    }
	private:
	    void helper(vector<int> &candidates, int target, vector<std::vector<int> > &res, vector<int> &tmp, int ind) {
	        if (!target) {  //递归结束条件
	            res.push_back(tmp);
	            return;
	        }
	        for (int i = ind; i < candidates.size() && target >= candidates[i]; ++i) {
	            tmp.push_back(candidates[i]);
	            helper(candidates, target - candidates[i], res, tmp, i);
	            tmp.pop_back();
	        }
	    }
	};

## 题目二 Combination Sum II  

**题目描述:** 见[https://leetcode.com/problems/combination-sum-ii/description/](https://leetcode.com/problems/combination-sum-ii/description/)  
**大意:** 给一个集合C和一个目标数T，从C中找出所有独特的组合，使他们的和等于T。其中C中的每个数在每次集合里只能使用一次。  
**一些条件:** 所有的数为正整数，最后的答案的集合不能重复。  
**待实现函数：**  

    
	class Solution {  
	public:  
	    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {  
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;首先这道题与**I**的区别在于，C中可能出现重复的值，而且在每一次组合时，C中的每个值最多只能使用一次。  
&nbsp;&nbsp;&nbsp;&nbsp;基于上题的解题过程，至于C中的每个值在每次组合中只能使用一次很好解决，我们只要在下次递归时```combinationSum(candidates, target - candidates[i], res, tmp, i);```修改i为i + 1即可，若仅作这样的修改，若C中含有重复的数时，在最终的答案中会出现重复的集合,比如C=[1,1,2,3], T=6,那么最后的结果会含有这样的答案[[1,2,3], [1,2,3]]。  
&nbsp;&nbsp;&nbsp;&nbsp;出现这个重复集合的原因在于我们找到[1,2,3]答案后，再次从头开始寻找时(即tmp为空时)，会将第二个1加入tmp，此时再次递归，就可能会找到一些重复的答案，这样我们只要在判断下次遍历时，加个条件判断去除这个情况即可避免。  

**解题源码：**  

	class Solution {
	public:
	    vector<vector<int> > combinationSum2(vector<int> &candidates, int target) {
	        sort(candidates.begin(), candidates.end());
	        vector<vector<int> > res;  //最终的结果
	        vector<int> tmp;  //递归查找过程中记录的集合
	        helper(candidates, target, res, tmp, 0);  //0表示从下标0开始
	        return res;
	    }
	private:
	    void helper(vector<int> &candidates, int target, vector<std::vector<int> > &res, vector<int> &tmp, int ind) {
	        if (!target) {  //递归结束条件
	            res.push_back(tmp);
	            return;
	        }
	        for (int i = ind; i < candidates.size() && target >= candidates[i]; ++i) {
                if (i == ind || candidates[i] != candidates[i - 1]) {  //去重条件
                    tmp.push_back(candidates[i]);
	                helper(candidates, target - candidates[i], res, tmp, i + 1);  //C中的数只能使用一次
	                tmp.pop_back();
                }
	        }
	    }
	};

## 题目三 Combination Sum III  

**题目描述:** 见[https://leetcode.com/problems/combination-sum-iii/description/](https://leetcode.com/problems/combination-sum-iii/description/)  
**大意:** 找出所有k个数的集合，它们的和等于n，其中可用的数为1-9。  
**待实现函数：**  

    
	class Solution {  
	public:  
	    vector<vector<int>> combinationSum3(int k, int n) {  
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;和之前题比较，其实C=[1..9], T=n，但是不同之处在于这里对每次组合的结果的个数进行了限定，即只能为k个数。   
&nbsp;&nbsp;&nbsp;&nbsp;这里只要加入k个数的限制，并且改变一下条件即可。```target >= i * need + need * (need - 1) / 2```，意思是当从i开始，需要need个数时，target必须要满足大于等于i+(i+1)+...+(i+need-1)  

**解题源码：**  

	class Solution {
	public:
	    vector<vector<int> > combinationSum3(int k, int n) {
	        vector<vector<int> > res;
	        vector<int> tmp;
	        helper(n, res, tmp, 1, k);
	        return res;
	    }
	private:
	    void helper(int target, vector<vector<int> > &res, vector<int> &tmp, int ind, int need) {
	        if (!target) {
	            res.push_back(tmp);
	            return;
	        }
	        else if (!need)
	            return;
	        for (int i = ind; i < 10 && target >= i * need + need * (need - 1) / 2; ++i) {
	            tmp.push_back(i);
	            helper(target - i, res, tmp, i + 1, need - 1);
	            tmp.pop_back();
	        }
	    }
	};

## 题目四 Combination Sum IV  

**题目描述:** 见[https://leetcode.com/problems/combination-sum-iv/description/](https://leetcode.com/problems/combination-sum-iv/description/)  
**大意:** 给定一个无重复的正整数集合C和一个正整数T，从C中找出所有的可能组合，使其和为T，输出这个可能的组合数。  
**待实现函数：**  

    
	class Solution {  
	public:  
	    int combinationSum4(vector<int>& nums, int target) {  
	    }  
	};  
    
  
**解题思路:**  
&nbsp;&nbsp;&nbsp;&nbsp;之前的题目均是找出这样的组合，而这里仅仅只要找出可能的组合数即可。另外需要注意的是，这里特别强调不同序列，结果就算不同，而之前均只算一种。     
&nbsp;&nbsp;&nbsp;&nbsp;看完题目，第一感觉就是和Combination Sum差不多，只需要稍加修改即可，但是会超时(见源码一)。  
&nbsp;&nbsp;&nbsp;&nbsp;既然超时的话，就只能再想方法，很自然的想到一种记录中间值的递归方法，就是把中间一些计算结果记录下来，避免重复计算。这里使用vector<int> tt来记录。  
&nbsp;&nbsp;&nbsp;&nbsp;另外还可以使用动态规划的方法，而其实上面的解法二就有着动态规划的雏形。  
**解题源码一：**  (超时)

	class Solution {
	public:
	    int combinationSum4(vector<int>& nums, int target) {
	        sort(nums.begin(), nums.end());
	        int res = 0;  //最终的结果
	        helper(nums, target, res);
	        return res;
	    }
	    
	    void helper(vector<int>& nums, int target, int& res){
	        if (!target) {  //递归结束条件
	            res++;
	            return;
	        }
	        for (int i = 0; i < nums.size() && target >= nums[i]; ++i) {
	            helper(nums, target - nums[i], res);
	        }
	    }
	};

**解题源码二：**  

	class Solution {
	public:
	    int combinationSum4(vector<int>& nums, int target) {
	        vector<int> tt(target + 1, -1);  //记录中间值 -1表示还没有计算出来
	        tt[0] = 1;
	        return helper(nums, target, tt);
	    }
	    
	    int helper(vector<int>& nums, int target, vector<int>& tt){
	        if(tt[target] != -1){  //记录有值，直接返回
	            return tt[target];
	        }
	        
	        int res = 0;
	        for(int i = 0; i < nums.size(); i++){  //遍历nums集合 计算所有可能
	            if(target >= nums[i]){
	                res += helper(nums, target - nums[i], tt);
	            }
	        }
	        
	        tt[target] = res;
	        return res;
	    }
	};