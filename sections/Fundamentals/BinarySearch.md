## 二分查找

```angularjs
function BinarySearch(arr,key){
  let lo = 0,hi = arr.length-1;
  while(lo<hi){
    let mid = lo + parseInt((hi - lo)/2);
    if(arr[mid] == key){
      return mid;
    }else if(arr[mid] < key){
      lo = mid +1
    }else{
      hi = mid-1
    }
  }
  return -1;
}
```

### 使用递归的二分查找

```angularjs
function BinarySearchRecursion(array,key){
  return RankRecursion(0,array.length-1);
  function RankRecursion(lo,hi){
    var mid = lo + parseInt((hi-lo)/2);
    if(key == array[mid]){
      return mid
    }else if(key > array[mid]){
      return RankRecursion(mid+1,hi);
    }else{
      return RankRecursion(lo,mid-1);
    }
    return -1
  }
}
```
