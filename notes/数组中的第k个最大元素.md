### 题目
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5

示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4

说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

### 题解
思考：   
查找数组中第k个最大元素，就先把数组排序，如果较优排序就使用快速排序，然后排序后返回对应元素即可
```php
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return Integer
     */
    function findKthLargest($nums, $k) {
        $this->quicksort($nums, 0, count($nums)-1);
        return $nums[count($nums)-$k];
    }
    
    //快速排序
    public function quicksort(&$arr, $left, $right){
        if($left < $right){
            $this->dealPivot($arr, $left, $right);
            $pivot = $right-1;
            $i = $left;
            $j = $right - 1;
            while(true){
                while($arr[++$i] < $arr[$pivot]){
                }
                while($arr[--$j] > $arr[$pivot]){
                }
                if($i<$j){
                    $this->swap($arr, $i, $j);
                }else{
                    break;
                }
            }
            if($i<$right){
                $this->swap($arr, $i, $right-1);
            }
            $this->quicksort($arr, $left, $i-1);
            $this->quicksort($arr, $i+1, $right);
        }
    }
    
    private function dealPivot(&$arr, $left, $right){
        $mid = floor(($left + $right) / 2);
        if($arr[$left] > $arr[$right]){
            $this->swap($arr, $left, $right);
        }
        if($arr[$left] > $arr[$mid]){
            $this->swap($arr, $left, $mid);
        }
        if($arr[$mid] > $arr[$right]){
            $this->swap($arr, $mid, $right);
        }
        $this->swap($arr, $mid, $right-1);
    }

    private function swap(&$arr, $i, $j){
        $temp = $arr[$i];
        $arr[$i] = $arr[$j];
        $arr[$j] = $temp;
    }
    
    
    //冒泡排序
    // function bubbleSort(&$nums){
    //     $count = count($nums);
    //     for($i = 0;$i<$count;$i++){
    //         $sign = 0;
    //         for($j=0;$j<$count-$i-1;$j++){
    //             if($nums[$j] < $nums[$j+1]){
    //                 $temp=$nums[$j+1];
    //                 $nums[$j+1]=$nums[$j];
    //                 $nums[$j]=$temp;
    //                 $sign=1;
    //             }
    //         }
    //         if(empty($sign)){
    //             break;
    //         }
    //     }
    // }
}
```
