---
layout: post
title:  "Algorithm day 2 blog, my first blog"
date:   2023-02-16 23:25:51 +0000
categories: jekyll update
---

Today, I handled 3 algorithm problems: 
1.Leetcode 977. Squares of a Sorted Array

Given an integer array nums sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Example:

{% highlight ruby%}
Input: nums = [-4,-1,0,3,10]
Output: [0,1,9,16,100]
Explanation: After squaring, the array becomes [16,1,0,9,100].
After sorting, it becomes [0,1,9,16,100].
{% endhighlight %}

I use a two pointers way, with code as below:

{% highlight ruby %}
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for (int i=0;i<nums.size();i++)
        {
            nums[i]*=nums[i];
        }
        int forward=0;
        int back=nums.size()-1;
        int j = nums.size()-1;
        vector<int> result(nums.size(),0);
        while (forward != back)
        {
            if (nums[forward]>=nums[back])
            {
                result[j--]=nums[forward++];
            }
            else
            {
                result[j--]=nums[back--];
            }
        }
        result[0]=nums[forward];
        return result;
    }
};
{% endhighlight %}
The time complexity is O(n).

2.Leetcode 209. Minimum Size Subarray Sum

Given an array of positive integers nums and a positive integer target, return the minimal length of a 
subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

Example:

{% highlight ruby%}
Input: target = 7, nums = [2,3,1,2,4,3]
Output: 2
Explanation: The subarray [4,3] has the minimal length under the problem constraint.
{% endhighlight %}

I use a two pointers way, also called moving sliding window.

{% highlight ruby %}
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int i = 0;
        int j = 0;
        int sum=0;
        int length = INT_MAX;
        for (j=0;j<nums.size();j++)
        {
            sum+=nums[j];
            while (sum>=target)
            {
                length =  length < (j-i+1) ? length : (j-i+1) ;
                sum-=nums[i++];
            }
        }
        return length == INT_MAX ? 0 : length;
    }
};
{% endhighlight %}
Time complexity is O(n)

3.59. Spiral Matrix II
Given a positive integer n, generate an n x n matrix filled with elements from 1 to n2 in spiral order.
Example:

{% highlight ruby%}
Input: n = 3
Output: [[1,2,3],[8,9,4],[7,6,5]]
{% endhighlight %}

I did this before, it is all about details at edges, corners and the middle part.
{% highlight ruby %}
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        vector<vector<int>> SM(n, vector<int>(n, 0)); // 使用vector定义一个二维数组
        int startx=0;
        int starty=0;
        int loop=n/2;
        int mid=n/2;
        int count=1;
        int offset=1;
        int i,j =0;
        while (loop--){
            i =startx;
            j = starty;
            for (j=starty;j<n-offset;j++){
                SM[i][j]=count++;
            }
            for (i=startx;i<n-offset;i++){
                SM[i][j]=count++;
            }
            for (;j>starty;j--){
                SM[i][j]=count++;
            }
            for (;i>startx;i--){
                SM[i][j]=count++;
            }
            offset+=1;
            startx++;
            starty++;
        }
        if (n%2==1){
            SM[mid][mid]=count;
        }
        return SM;
    }
};
{% endhighlight %}

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
