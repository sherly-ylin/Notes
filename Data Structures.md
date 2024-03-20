

## Array
- a contiguous memory space
Index/get: O(1)
Insert/write: O(1)
Delete: O()
## Linked List



Array vs Linked List

|        | Unsorted Array  | Sorted Array | Sorted LL |
| ------ | ------------- | -------------- | --------- |
| Search | O(N) | O(Log N) | O(N)
| Insert | O(1) | O(N)     | O(N)
| Delete | O(1) | O(N)     | O(1)
| Memory | O(N) | O(N)     | 




## Stack 
First In Last Out (FILO)

## Queue
First In Last Out (FIFO)

## Heap

Hash Table

Tree
BST
Graph 



-----

### Searching & Sorting Algorithms
#### Linear Search: $O(n)$
#### Binary Search: $O(n)$

#### Bubble Sort: $O(n^2)$
- compare 2 adjacent element, swap as needed, move from left to right
- the largest bubbled to the end, sorted array expanding from the end to start
```java
int j = A.length;
for (int i = 0; i<j-1; i++){
    if(A[i]>A[i+1]){
        swap;
    }
    j--;
}
```


#### Selection Sort: $O(n^2)$
- split into sorted & unsorted subarrays, initially all unsorted 
- select the smallest from unsorted array and swap with the leftmost in unsorted, which then becomes part of sorted sorted subarray.
```java
int sorted = 0;
while(sorted<=A.length){
    int min = A[sorted], min_i = sorted,
    for (int i = sorted+1; i< A.length; i++){
        if(A[i]<min){
            min = A[i];
            min_i = i;
        }
        if (min_i > sorted ){
            A[min_i]= A[sorted+1];
            A[sorted+1]=min
        }
        sorted++;
    }
}
```
#### Insertion Sort: $O(n^2)$
- split into 2 sorted & unsorted subarrays, initially the 1st element is sorted
- insert element in the unsorted into sorted one by one
```java
for (int i = 1; i<A.length; i++){
    key = A[i];
    j = i-1;
    //sliding larger element to the right
    while (j>=0 && A[j]>key){
        A[j+1]= A[j];
        j = j-1
    }
    A[j+1]=key;
}
```
#### Merge Sort: $O(n log n)$
- keep split in half until can't be splited
- merge and sort smaller sorted subarray into a single one
Pseudocode
```
mergesort(A){
    n = A.length
    if (n==1){
        return A;
    }
    k = n/2;
    AL = mergesort(A[1:k]), AR = (A[k:n])

    B = [];
    i = 1, j = 1;
    while (i<=k && j <=n-k){
        if (AL[i]<AR[j]){
            B.append(AL[i]); i++;
        }else{
            B.append(AR[j]); j++;
        }
    }
    # if AL,AR diff len, append the remaining element
    if (i>k){ 
        B.append(AR[j:end]) 
    }else{
        B.append(AL[i:end]) 
    }
    return B;$$
}   
```

#### Quick Sort: $O(n^2)$
- recursively pick pivots, left values < pivot < right values
```

```

