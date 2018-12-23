# 快速排序

>快速排序以其实现简单和在日常业务中对数据处理比其他的排序算法更快的优点在业务中应用广泛。它只需要一个很小的辅助栈，就能够以NlogN的时间复杂度
进行排序。尽管其内循环比大多数排序算法都要短小，在实际应用中也非常容易将其时间复杂度变成N^2，接下来我们来看看其实际应用。

```angularjs
let quick_sort = (arr,left,right) => {
  if(left > right) return ;
  let j = partition(arr,left, right);
  quick_sort(arr,left,j-1);
  quick_sort(arr,j+1,right);
}

let partition = (arr,l,r) => {
  let v = arr[l],
      j = l;
  for(let k=l+1;k<=r;k++){
    if(arr[k] < v){
      let temp = arr[k];
      arr[k] = arr[j+1];
      arr[j+1] = temp;
      j++;
    }
  }
  arr[l] = arr[j];
  arr[j] = v;
  return j;
}
```
快速排序生成的递归树比归并排序的要差，在最差的情况下会变成N^2的时间复杂度
所以需要随机选取一个中间变量
```angularjs
let partition = (arr,l,r) => {
  let ran = Math.floor(Math.random() * (r-l+1)) + l;
  let temp1 =arr[ran];
  arr[ran] = arr[l];
  arr[l] = arr[temp1];
  let v = arr[l],
      j = l;
  for(let k=l+1;k<=r;k++){
    if(arr[k] < v){
      let temp = arr[k];
      arr[k] = arr[j+1];
      arr[j+1] = temp;
      j++;
    }
  }
  arr[l] = arr[j];
  arr[j] = v;
  return j;
}
```

