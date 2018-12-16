# 归并排序

### 自顶向下的归并排序
```angularjs
let _merge(leftArray,rightArray){
  let result = [];
  while(leftArray.length && rightArray.length){
    result.push(leftArray[0] <= rightArray[0] ? leftArray.shift() : rightArray.shift());
  }
  return result.concact(leftArray).concact(rightArray);
}

let mergeSort(array){
  if(array.length<2) return array;
  let mid = Math.floor(array.length / 2);
  return _merge(mergeSort(array.slice(0,mid)),mergeSort(array.slice(mid)));
}
```
