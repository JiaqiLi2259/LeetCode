# [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/)
-------------
## Description  
Given an array nums of n integers where n > 1,  return an array output such that *output[i]* is equal to the product of all the elements of nums **except** *nums[i]*.  

**Example:**  
```
Input:  [1,2,3,4]  

Output: [24,12,8,6]
```
**Note:**  
Please solve it `without division` and in O(n).
___________
## Thought
Instead of division, we use **two arrays** to store the products of all left elements and all right elements by **i<sub>th</sub> nums[i]**.    
So the result will be the product of two elements of the same position in array *left* and array *right*.
___________
## Code
```Java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int len = nums.length;
        int[] result = new int[len];
        int[] left = new int[len];
        int[] right = new int[len];
        left[0] = 1; right[len-1] = 1;
        for(int i = 0; i < len - 1; i++){  // product of all left elements
            left[i+1] = left[i] * nums[i];
        }
        for(int i = len - 1; i > 0; i--){  // product of all right elements
            right[i-1] = right[i] * nums[i];
        }
        for(int i = 0; i < len; i++){
            result[i] = left[i] * right[i];
        }
        return result;
    }
} 
```
