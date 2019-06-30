# [Remove Duplicates from Sorted Array I](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
-------------
## Description-1  
Given a sorted array nums, remove the duplicates **in-place** such that each element appear ***only once*** and return the new length.  

Do not allocate extra space for another array, you must do this by modifying the input array **in-place** with O(1) extra memory  
**Example:**  
```
Given nums = [0,0,1,1,1,2,2,3,3,4],  

Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.  

It doesn't matter what values are set beyond the returned length.
```
___________
## Thought-1
大loop是：nums[i]被覆盖 + 找到下一个非重复元素  
小loop是：找到下一个非重复元素（注意要判断指针是否越界）
___________
## Code-1
```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        if(nums.length < 1){
            return 0;
        }
        int i, j, len, temp;
        len = nums.length;
        i = -1; j = 0;
        while(j <= len - 1){  //大loop
            temp = nums[j];
            i += 1;
            nums[i] = temp;
            while(j <= len-1 && nums[j] == temp){  //小loop
                j += 1;
            }
        }
        return i+1;
    }
}
```
# [Remove Duplicates from Sorted Array II](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/)
-------------
## Description-2  
Given a sorted array nums, remove the duplicates **in-place** such that duplicates appeared ***at most twice*** and return the new length.  

Do not allocate extra space for another array, you must do this by modifying the input array **in-place** with O(1) extra memory.  
**Example:**  
```
Given nums = [0,0,1,1,1,1,2,3,3],  

Your function should return length = 7, with the first seven elements of nums being modified to 0, 0, 1, 1, 2, 3 and 3 respectively.  

It doesn't matter what values are set beyond the returned length.
```
___________
## Thought-2
大loop是：nums[i]被覆盖 + 找到下一个非重复元素（counter的值要赋值为0）  
小loop是：找到下一个非重复元素（注意要判断counter的值和指针是否越界）
___________
## Code-2
```Java
class Solution {
    public int removeDuplicates(int[] nums) {
        int i, j, temp, counter;
        int len = nums.length;
        if(len <= 2){
            return len;
        }
        i = -1; j = 0; counter = 0;
        while(j < len){
            temp = nums[j];
            i += 1;
            nums[i] = temp;
            j += 1;
            counter += 1;
            while(j < len && nums[j] == temp){
                if(counter >= 2){  //判断counter的值
                    j++;
                }else{
                    i += 1;
                    nums[i] = temp;
                    j += 1;
                    counter += 1;
                }
            }
            if(j < len){
                counter = 0;  //counter值重新赋0
            }
        }
        return i+1;
    }
}
```
