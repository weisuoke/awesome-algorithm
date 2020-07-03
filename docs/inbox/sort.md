# 排序算法

### 通用函数

```js
function swap(array, left, right) {
  var rightValue = array[right]
  array[right] = array[left]
  array[left] = rightValue
}
```

## 快速排序

快速排序是处理大数据集最快的排序算法之一。它是一种分而治之的算法，通过递归的方式将数据依次分解为包含较小元素和较大元素的不同子序列。该算法不断重复这个步骤直到所有数据都是有序的。

这个算法首先要在列表中选择一个元素作为基准值(pivot)。数据排序围绕基准值进行，将列表中小于基准值的元素移到数组的底部，将大于基准值的元素移到数组的顶部。

## 选择排序

> 一句话：找到数组中最小或最大的元素，依次放入指定的位置。

选择排序从数组的开头开始，将第一个元素和其他元素进行比较。检查完所有元素后，最小的元素会被放到数组的第一个位置，然后算法会从第二个位置继续。这个过程一直进行，当进行到数组的倒数第二个位置时，所有的数据便完成了排序。

选择排序会用到嵌套循环。外循环从数组的第一个元素移动到倒数第二个元素;内循环从第二个数组元素移动到最后一个元素，查找比当前外循环所指向的元素小的元素。每次内循环迭代后，数组中最小的值都会被赋值到合适的位置。

```js
function quickSort(arr) {
  if (arr.length == 0) {
    return [];
  }
  var left = [];
  var right = [];
  var pivot = list[0];
  for (var i = 1; i < arr.length; i++) {
    if (arr[i] < pivot) {
      left.push(arr[i])
    } else {
      right.push(arr[i])
    }
  }
  return quickSort(left).concat(pivot, quickSort(right));
}
```

快速排序算法非常适用于大型数据集合;在处理小数据集时性能反而会下降。

### 实现

```js
// selectionSort()
function selectionSort(dataStore) {
  var min, temp;
  for (var outer = 0; outer <= dataStore.length - 2; ++outer) {
    min = outer;
    // 线性查找最小值
    for (var inner = outer + 1; inner <= dataStore.length - 1; ++inner) {
      if (dataStore[inner] < dataStore[min]) {
        min = inner
      }
      swap(dataStore, outer, min)
    }
   }
}
```

## 归并排序

归并排序的命名来自它的实现原理:把一系列排好序的子序列合并成一个大的完整有序序列。从理论上讲，这个算法很容易实现。我们需要两个排好序的子数组，然后通过比较数据大小，先从最小的数据开始插入，最后合并得到第三个数组。然而，在实际情况中，归并排序还有一些问题，当我们用这个算法对一个很大的数据集进行排序时，我们需要相当大的空间来合并存储两个子数组。就现在来讲，内存不那么昂贵，空间不是问题，因此值得我们去实现一下归并排序，比较它和其他排序算法的执行效率。

### 自底向上归并排序算法

```js
function mergeSort(arr) {
  if (arr.length < 2) {
    return;
  }
  var step = 1;
  var left, right;
  while (step < arr.length) {
    left = 0;
    right = step;
    while (right + step <= arr.length) {
      mergeArrays(arr, left, left + step, right, right + step);
      left = right + step;
      right = left + step;
    }
    if (right < arr.length) {
      mergeArrays(arr, left, left + step, right, arr.length);
    }
    step *= 2;
  }
}

function mergeArrays(arr, startLeft, stopLeft, startRight, stopRight) {
  var rightArr = new Array(stopRight - startRight + 1);
  var leftArr = new Array(stopLeft - startLeft + 1);
  k = startRight;
  for (var i = 0; i < rightArr.length - 1; ++i) {
    rightArr[i] = arr[k];
    ++k;
  }
  k = startLeft;
  for (var i = 0; i < leftArr.length - 1; ++i) {
    leftArr[i] = arr[k];
    ++k;
  }

  rightArr[rightArr.length - 1] = Infinity; // 哨兵值 leftArr[leftArr.length-1] = Infinity; // 哨兵值 varm=0;
  varn = 0;
  for (var k = startLeft; k < stopRight; ++k) {
    if (leftArr[m] <= rightArr[n]) {
      arr[k] = leftArr[m];
      m++;
    } else {
      arr[k] = rightArr[n];
      n++;
    }
  }
  print("left array - ", leftArr);
  print("right array - ", rightArr);
}
var nums = [6, 10, 1, 9, 4, 8, 2, 7, 3, 5];
print(nums);
print();
mergeSort(nums);
print();
print(nums);
```