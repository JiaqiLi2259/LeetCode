# [Two Sum](https://leetcode.com/problems/two-sum/)
-------------
## Description  
Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.  
You may assume that each input would have **exactly one solution**, and you may not use the same element twice.  
**Example:**  
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```
___________
## Thought
Use HashMap, in which key: the target minus the current element *nums[i]*, value: the index *i*.    
The reason why we can use Hashmap is that we assume each input would have **exactly one solution**.
___________
## Code
```Java
import java.util.HashMap;
class Solution {
   
    public int[] twoSum(int[] n, int target) {
        if(n == null || n.length < 2){
            return new int[] {};  //return null
        }
        else{
            int len = n.length;
            HashMap <Integer, Integer> map = new HashMap<>();
            for (int i = 0; i < len; i++){
                if (map.containsKey(n[i])){
                    return new int[] {map.get(n[i]), i};
                }
                else{
                    map.put(target - n[i], i);
                }
            }
            return new int[] {};  //return null
        }
    }
   
}
```
