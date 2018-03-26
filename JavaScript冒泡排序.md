---
title: JavaScript冒泡排序
date: 2017-04-06 19:40:09
tags: [算法,JavaScript]
categories: [前端,JavaScript]
---
```js
function BubbleSort(arr) {
    for (let i = 0; i < arr.length - 1; i++) {
        for (let j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j + 1] < arr[j]) {
                let temp = arr[j + 1];
                 arr[j + 1] = arr[j]
                 arr[j] = temp;                        
             }
        }
    }
     return arr;
}
let arrs = [1, 8, 6, 3, 4, 9, 7];
console.log(BubbleSort(arrs));//[1, 3, 4, 6, 7, 8, 9]
```