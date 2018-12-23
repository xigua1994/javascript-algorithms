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

### 自底向上的归并排序

```angularjs
var arr = [];
let sort = () => {
  let len = arr.length;
  for(let i=1;i<len;i=2 * i){
    for(let j = 0;j<len - i;j+=2 * i){
      merge(arr,j,j+i-1,Math.min(j+2*i-1,len-1));
    }
  }
}

let merge = (a,lo,mid,hi) => {
  let i = lo,j = mid+1,aux = [];
  for(let k = lo;k<=hi;k++){
    aux[k] = a[k];
  }
  for(let k=lo;k<=hi;k++){
    if(i>mid){
      a[k] = aux[j++]
    }else if(j>hi){
      a[k] = aux[i++]
    }else if(aux[j]<aux[i]){
      a[k] = aux[j++]
    }else{
      a[k] = aux[i++];
    }
  }
}
```
