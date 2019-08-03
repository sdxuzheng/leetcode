### 题目
给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点。

示例：

给定一个链表: 1->2->3->4->5, 和 n = 2.

当删除了倒数第二个节点后，链表变为 1->2->3->5.
说明：

给定的 n 保证是有效的。

进阶：

你能尝试使用一趟扫描实现吗？

### 思路
1、因为题目只告诉了链表的头元素，所以想既删除指定元素又返回头元素，那么必定需要遍历知道链表全部元素才可以

2、如果想遍历次数只有一次同时又想消耗时间最短，那么就是把链表内容存储到哈希表中，时间复杂度O(1)

3、除头元素外需要删除谁，就把该元素的前一个元素的next指向该元素的后一个元素即可；对于头元素则直接将该头元素删除返回第二个元素即可

### 题解
```php
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $n
     * @return ListNode
     */
    function removeNthFromEnd($head, $n) {
        $hash = [];
        do{
            $hash[] = $head;
            $head = $head->next;
        }while(!empty($head));
        $count = count($hash);
        $key = $count - $n;
        if($key !== 0){
            $hash[$key - 1]->next = $hash[$key + 1];
            $head = $hash[0];
        }else{
            unset($hash[0]);
            $head = $hash[1];
        }
        
        return $head;
    }
}
```
