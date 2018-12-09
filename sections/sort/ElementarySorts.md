# 初级排序算法

## 选择排序

最简单的排序算法就是：先将最小的元素与第一位元素交换位置，再在剩下的元素找出最小的与第二位元素交换位置，如此往复，整个数组就变成有序的了。
```angular2html
let selectSort = (array) => {
  let len = array.length;
  for(let i=0 ; i<len ; i++){
    let minIndex = i,
        minValue = array[i];
    for(let j=i+1 ; j<len ; j++){
      if( array[minIndex] > array[j]){
        minIndex = j;
        minValue = array[j]
      }
    }
    arr[minIndex] = array[i];
    array[i] = minValue;
  }
  return array;
}
```

选择排序有两个非常重要的特点：
* 运行时间与输入无关，无论数组的初始状态是否是有序的，比较次数都不会发生变化，都需要进行n(n-1)/2次比较。
* 数据移动最多为n-1次，数据的移动在算法中是最少的。


