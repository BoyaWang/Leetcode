# Leetcode
Leetcode solution in C++ and notes  

## Summary of Algorithm Interview Questions  
136. Single Number 只出现一次的数  
Given a **non-empty** array of integers, every element appears twice except for one. Find that single one.  
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?  
Eg.  
Input: [2,2,1]  
Output: 1  
``` 
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        // ^ 是C++中的异或运算符。一个数字异或自身会为0，在数组中可以遍历寻找那个只出现一次的数。
        int res = 0;
        for (int i=0; i<nums.size(); i++){
            res = res ^ nums[i]; 
        }
        return res;
    }
};  
```  
169. Majority Element 求众数  
Given an array of size n, find the majority element. The majority element is the element that appears **more than** `⌊ n/2 ⌋` times.  
You may assume that the array is non-empty and the majority element always exist in the array.  
Eg.  
Input: [3,2,3]  
Output: 3  
```  
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        int n = nums.size();
        if (n % 2 == 0) return nums[n / 2]; // 巧解，因为众数多于n/2
        else return nums[(n - 1) / 2];
    }
};
```  
240. Search a 2D Matrix II 搜索二维矩阵II  
Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:  
Integers in each row are sorted in ascending from left to right.  
Integers in each column are sorted in ascending from top to bottom.  
Eg.  
>[
>  [1,   4,  7, 11, 15],  
>  [2,   5,  8, 12, 19],  
>  [3,   6,  9, 16, 22],  
>  [10, 13, 14, 17, 24],  
>  [18, 21, 23, 26, 30]  
>]  
Given target = 5, return true.  
Given target = 20, return false.  
```  
\\ 总体思想是从左下角开始，如果目标比它小，向上，如果目标比它大，向右
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int row = matrix.size();
        if (row == 0) return false;
        int col = matrix[0].size();
        if (col == 0) return false;
        int row_n = row - 1;
        int col_n = 0;
        while ((row_n >= 0) && (col_n <= col - 1)){
            if (matrix[row_n][col_n] == target) return true;
            else if (matrix[row_n][col_n] < target) col_n++;
            else if (matrix[row_n][col_n] > target) row_n--;
        }
        return false;       
    
    }
};
```  
88. Merge Sorted Array 合并两个有序数组  
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.  
The number of elements initialized in nums1 and nums2 are m and n respectively.  
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.  
Eg.  
Input:  
nums1 = [1,2,3,0,0,0], m = 3  
nums2 = [2,5,6],       n = 3  
Output: [1,2,2,3,5,6]  
```
// 从结尾开始，放入两个数组中较大的一个；
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        int k = nums1.size() - 1;
        while ((m > 0)&&(n > 0)) {
            if (nums1[m - 1] >= nums2[n - 1]){
                swap(nums1[k], nums1[m - 1]);
                m--;
                k--;
            }
            else if (nums1[m - 1] < nums2[n - 1]){
                nums1[k] = nums2[n - 1];
                n--;
                k--;
            }
        }
        if ((m == 0)&&(n != 0)){
            while (n != 0){
                nums1[k] = nums2[n - 1];
                k--;
                n--;
            }
        }
        else if ((n == 0)&&(m != 0)){
            while (m != 0){
                swap(nums1[k], nums1[m - 1]);
                k--;
                m--;
            }
        }
    }
};
```  
