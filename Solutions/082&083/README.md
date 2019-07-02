# [Remove Duplicates from Sorted List I](https://leetcode.com/problems/remove-duplicates-from-sorted-list/)
-------------
## Description-1  
Given a sorted linked list, delete all duplicates such that each element appear ***only once***.    
**Example:**  
```
Input: 1->1->2  
Output: 1->2  
Input: 1->1->2->3->3  
Output: 1->2->3
```
___________
## Thought-1
不用像处理数组那样重置每个节点的数值，而是改变节点的指向  
prev是选中的节点，p是待检查的节点（注意返回前最后一个节点要指向空）
___________
## Code-1
```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode prev, p;
        if(head == null || head.next == null){
            return head;
        }
        prev = head;
        p = head.next;
        while(p != null){
            if(prev.val == p.val){
                p = p.next;
            }else{
                prev.next = p;
                prev = p;
                p = p.next;
            }
        }
        prev.next = null;  //最后的节点指向空
        return head;
    }
}
```
# [Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/)
-------------
## Description-2  
Given a sorted linked list, delete all nodes that have duplicate numbers, leaving only ***distinct numbers*** from the original list. 
**Example:**  
```
Input: 1->2->3->3->4->4->5  
Output: 1->2->5  
Input: 1->1->1->2->3  
Output: 2->3
```
___________
## Thought-2
prev始终保持是候选的节点，是否被选要看其后p的值：  
若相同(flag=1)则找到下一个新出现值，更新prev和p；若不同(flag=0)则记录prev，直接更新prev和p  
(注意返回前最后一个节点要指向空)  
___________
## Code-2
```Java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        ListNode prev, p, newHead, newPrev;
        int temp, flag;
        if(head == null || head.next == null){
            return head;
        }
        newHead = null;
        newPrev = null;
        flag = 0;
        prev = head;
        p = head.next;
        while(p!=null){
            temp = prev.val;
            while(p !=null && p.val == temp){
                p = p.next;
                flag = 1;
            }
            if(flag == 0){
                if(newHead == null){
                    newHead = prev;
                    newPrev = newHead;
                }else{
                    newPrev.next = prev;
                    newPrev = prev;
                }
            }
            prev = p;
            if(p != null){
                p = p.next;
                flag = 0;
            }
        }
        if(newHead != null){
            newPrev.next = prev;  //最后的节点指向空
        }else{
            newHead = prev;
        }
        return newHead;
    }
}
```
