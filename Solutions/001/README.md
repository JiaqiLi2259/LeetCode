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
## Thought-1
Use HashMap, in which key: the target minus the current element *nums[i]*, value: the index *i*.    
The reason why we can use Hashmap is that we assume each input would have **exactly one solution**.
___________
## Code-1
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
___________
## Thought-2
Sort the array in advance and use two pointers, move front or back pointer according to comparison between target value and the sum of values which two pointers point to.
___________
## Code-2
```Java
class Solution {
    class point{
        int index, value;
        public point(int a, int b){
            this.index = a;
            this.value = b;
        }
    }
    public int[] twoSum(int[] n, int target) {
        if(n == null || n.length < 2){
            return new int[] {};
        }
        else{
            int len = n.length;
            Solution s = new Solution();
            point[] p =new point[len];
            for (int i = 0; i < len; i++){
                p[i] = s.new point(i, n[i]);
            }
            quicksort(p, 0, len-1);
            int low =0, high = len -1 ;
            while (low < high){
                int result = p[low].value + p[high].value;
                if (result== target){
                    return new int[] {Math.min(p[low].index,p[high].index), Math.max(p[low].index,p[high].index)};
                }
                else if(result < target){
                    low += 1;
                }else {
                    high -= 1;
                }
            }
            return new int[] {};
        }
    }
    public void quicksort(point[] A, int p, int r){
        if (p < r){
            int q = partition(A, p, r);
            quicksort(A, p, q-1);
            quicksort(A, q+1, r);
        }
    }
    public  int partition(point[] A, int p, int r){
        point pivot = A[r];
        int i = p - 1, j;
        for (j = p; j <= r-1; j++){
            if (A[j].value <= pivot.value){
                i += 1;
                point temp;
                temp = A[j];
                A[j] = A[i];
                A[i] = temp;
            }
        }
        A[r] = A[i+1];
        A[i+1] = pivot;
        return i+1;
    }
}
```
