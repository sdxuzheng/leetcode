### 题目
合并 k 个排序链表，返回合并后的排序链表。请分析和描述算法的复杂度。

示例:

输入:
[
  1->4->5,
  1->3->4,
  2->6
]
输出: 1->1->2->3->4->4->5->6

### 思路
其实就是遍历所有链表，将链表放入数组，然后对数组进行排序，排序完成后再根据数组生成新的链表

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
     * @param ListNode[] $lists
     * @return ListNode
     */
    function mergeKLists($lists) {
        $arr = [];
        foreach($lists as $key => $value){
            while(!empty($value)){
                $arr[] = $value;
                $value = $value->next;
            }
        }
        $count=count($arr);
        for($i=0;$i<$count;$i++){
            for($j=0;$j<$count-$i-1;$j++){
                if($arr[$j]>$arr[$j+1]){
                    $temp=$arr[$j+1];
                    $arr[$j+1]=$arr[$j];
                    $arr[$j] = $temp;
                }
            }
        }
        $first=null;
        for($i=0;$i<$count;$i++){
            $l3 = new ListNode($arr[$i]->val);
            if(!empty($last)){
                $last->next = $l3;
                $last = $last->next;
            }else{
                $last = $l3;
                $first = $l3;
            }
        }
        return $first;
    }
}
```
