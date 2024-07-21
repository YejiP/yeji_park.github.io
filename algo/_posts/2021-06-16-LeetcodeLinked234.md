# Leetcode 234) Palindrome Linked List

![image](https://user-images.githubusercontent.com/37058233/122303349-41e89d00-ceb8-11eb-999c-a63c90056d83.png)

# 내 풀이

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        if(head.next==null){
            return true;
        }
        //중앙 찾아서 앞부분은스택에 저장을하고, pop하면서 비교한다.
        ListNode dummy = head;
        int cnt=0;
        while(dummy!=null){
            dummy = dummy.next;
            cnt++;
        }
        dummy= head;
        //삼항 연산자 사용, odd 체크
        int div = cnt/2;
        Stack<Integer> a = new Stack<>();
        for(int _i=0;_i<div;_i++){
            a.push(dummy.val);
            dummy=dummy.next;
        }
        boolean odd=(cnt%2==1)? true: false;
        if(odd){
            dummy=dummy.next;
        }
        while(a.pop()==dummy.val){
            dummy = dummy.next;
            if(a.empty()){
                break;
            }
            }
        if(a.empty() && dummy==null){
            return true;
        }
        return false;
        }
    }
```

# 다른 답안

- slow, fast 포인터 테크닉을 사용해서 
  - fast가 끝에 닿을 때, slow는 중간에 닿는다.
  - 처음부터 중간까지의 리스트를 reverse하면서 순회한다.

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public boolean isPalindrome(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = null;
        while(fast!=null && fast.next!=null){
            fast = fast.next.next;
            ListNode temp = slow;
            slow = slow.next;
            temp.next = prev;
            prev = temp;
        }
        if(fast!=null){
            slow = slow.next;
        }
        while(slow!=null && prev!=null){
            if(slow.val!=prev.val){
                return false;
            }
            slow = slow.next;
            prev = prev.next;
        }
        return true;
    }
}
```

