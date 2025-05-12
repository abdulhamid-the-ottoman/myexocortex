---
created:
  - 2023-07-09 21:52
share: true
---

up::[ Heaps](NeetCode%20Index.md#^c810f8)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Design a class to find the `kth` largest element in a stream. Note that it is the `kth` largest element in the sorted order, not the `kth` distinct element.
> 
> Implement `KthLargest` class:
> 
> - `KthLargest(int k, int[] nums)` Initializes the object with the integer `k` and the stream of integers `nums`.
> - `int add(int val)` Appends the integer `val` to the stream and returns the element representing the `kth` largest element in the stream.
> 
> ![Pasted image 20230709215339.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230709215339.png)
> 
> **Constraints:**
> 
> - `1 <= k <= 104`
> - `0 <= nums.length <= 104`
> - `-104 <= nums[i] <= 104`
> - `-104 <= val <= 104`
> - At most `104` calls will be made to `add`.
> - It is guaranteed that there will be at least `k` elements in the array when you search for the `kth` element.


## 🔑 **Key Points of Understanding**
- the idea is to create a min heap and sort it then remove the kth element


# 🔍 Solutions

```C++
#include <vector>  
#include <iostream>  
  
using std::vector;  
using std::cout;  
using std::endl;  
  
class KthLargest {  
private:  
    int kth;  
    int size;  
    vector<int> heap;  
  
    int parent(int ind){  
        return (ind-1)/2;  
    }  
  
    int left(int ind){  
        return 2*ind + 1;  
    }  
  
    int right(int ind){  
        return 2*ind + 2;  
    }  
  
    bool exists(int ind){  
        return ind < size;  
    }  
  
    bool isValid(int ind){  
        return ind == 0 || heap[parent(ind)] < heap[ind];  
    }  
  
    void swap(int a, int b){  
        int tmp = heap[a];  
        heap[a] = heap[b];  
        heap[b] = tmp;  
    }  
  
    int swapup(int ind){  
        int pind = parent(ind);  
        swap(ind,pind);  
        return pind;  
    }  
  
    void upbubble(int ind){  
        if(!isValid(ind)){  
            upbubble(swapup(ind));  
        }  
    }  
  
    void addVal(int val){  
        heap.push_back(val);  
        upbubble(size);  
        size++;  
    }  
  
    int min2(int a, int b){  
        if(exists(a) && exists(b)){  
            return heap[a] > heap[b] ? b: a;  
        }  
        else{  
            if(exists(a)){  
                return a;  
            }  
            else{  
                return b;  
            }  
        }  
    }  
  
    int min3(int a, int b, int c){  
        return min2(min2(a,b),c);  
    }  
  
    void downbubble(int ind){  
        if(size > 0 ) {  
            int min = min3(ind, left(ind), right(ind));  
            if (min != ind) {  
                swap(min, ind);  
                downbubble(min);  
            }  
        }  
    }  
  
    void sort(){  
        while(size != 0){  
            swap(size-1,0);  
            size--;  
            downbubble(0);  
        }  
    }  
  
    int extract(int ind){  
        int val = heap[ind-1];  
        for(int i = ind-1; i < heap.size()-1 ; ++i){  
            heap[i] = heap[i+1];  
        }  
        heap.pop_back();  
        size = heap.size();  
        std::reverse(heap.begin(), heap.end());  
        return val;  
    }  
  
public:  
    KthLargest(int k, vector<int>& nums): kth(k), size(nums.size()), heap(nums) {  
        for(int i = 0 ; i < heap.size(); ++i){  
            upbubble(i);  
        }  
    }  
  
    int add(int val) {  
        addVal(val);  
        sort();  
        return extract(kth);  
    }  
};  
  
  
void kth_largest_test(){  
    vector<int> nums = {4, 5, 8, 2};  
    KthLargest kthLargest(3,nums );  
    cout << kthLargest.add(3) << endl;   // return 4  
    cout << kthLargest.add(5) << endl;   // return 5  
    cout << kthLargest.add(10) << endl;  // return 5  
    cout << kthLargest.add(9) << endl;   // return 8  
    cout << kthLargest.add(4) << endl;   // return 8  
}
```

# 🧠 Ideas about Problem

# 🔗 Related Applications

