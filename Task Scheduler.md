---
created:
  - 2023-07-11 18:36
share: true
---

up::[Heap](NeetCode%20Index.md#^c810f8)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
>  Given a characters array `tasks`, representing the tasks a CPU needs to do, where each letter represents a different task. Tasks could be done in any order. Each task is done in one unit of time. For each unit of time, the CPU could complete either one task or just be idle.
> 
> However, there is a non-negative integer `n` that represents the cooldown period between two **same tasks** (the same letter in the array), that is that there must be at least `n` units of time between any two same tasks.
> 
> Return the least number of units of times that the CPU will take to finish all the given task
> 
> ![Pasted image 20230711183746.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230711183746.png)
> 
> **Constraints:**
> 
> - `1 <= task.length <= 104`
> - `tasks[i]` is upper-case English letter.
> - The integer `n` is in the range `[0, 100]`.

## 🔑 **Key Points of Understanding**
 - calculate the frequencies of each type of task
	 - and start with the most frequent one and schedule others in between
	 - and go the next most frequent
- Example:
	-  \[A A A B B  C C\] n =1,  Let' s count the frequencies
	- \[3 2 2\] -> this is going to be our max heap
	- let's pop the first one at t = 0, our heap becomes \[2,2\]
		- and schedule 1 3-1=2  which can continue at t = 0 + 1 (current job to finish) + 1(cool off time (n)) = 2, we put it in our queue \[(2,2)\]
	- now we are t=1, we can schedule another one from our heap \[2, 2\] , our heap becomes \[2\]
		- we pop 2 and start one job, and we schedule 2-1 =1 at time t = 1+1 (current job to finish) + 1(cool off) = 3 and put it in our queue \[(2,2),(3,1)\]
	- now we are at t=2, we look at our queue, we pop it because the it activates at 2 and push it into our max heap \[2\] and our heap becomes \[2,2\]
		- we pop from our heap 2, our heap becomes \[2\]
		- we schedule one job and what remains it 2-1 = 1 job which can start running at t=2 + 1(job time) + 1(cool off) = 4, and we put it into the queue. \[(3,1),(4,1)\]
	- now we are at t=3, we check whether we have something scheduled at 3 in our queue,
		- we do, we pop it and add it to our heap \[2,1\] - > our heap becomes \[1\]
		- we pop from our heap 2 and schedule what remains 2-1 =1 job which can run at earliest t = 3 + 1 + 1 = 5, and add it to the queue \[(4,1),(5,1)\]
	- now we are at t= 4, we check our queue
		- pop from queue and add to the heap \[1,1\] 
		- pop from the heap (heap becomes \[1\]) and run 1-1 = 0 jobs no future scheduling
	- now we are at t=5, we check our queue
		- pop from the queue and add it to heap \[1,1\]
		- pop from the heap (heap becomes \[1\]) and run 1-1 = 0 jobs no future scheduling
	- Now we are at t=6, we check our queue 
		- since there is nothing at the queue, we look at the heap and pop from the heap (heap becomes \[\])
		- we run it the last job which will finish at 7.

# 🔍 Solutions

```C++
#include <algorithm>  
#include <iostream>  
#include <queue>  
#include <vector>  
#include <unordered_map>  
  
  
using std::queue;  
using std::vector;  
using std::cout;  
using std::endl;  
using std::unordered_map;  
  
class Solution {  
private:  
    vector<int> getFrequencies(const vector<char>& tasks){  
        vector<int> freq;  
        unordered_map<char,int> histogram;  
        for(auto & task:tasks){  
            if(histogram.contains(task)){  
                histogram[task]++;  
            }  
            else{  
                histogram[task] = 1;  
            }  
        }  
  
        for(auto & pair : histogram){  
            freq.push_back(pair.second);  
        }  
        return freq;  
    }  
  
    void schedule(queue<std::pair<int,int>>& future, vector<int>& heapschedule, int time){  
     if(!future.empty()){  
         std::pair<int,int> top = future.front();  
         if(time >= top.first){  
             heapschedule.push_back(top.second);  
             std::push_heap(heapschedule.begin(),heapschedule.end());  
             future.pop();  
         }  
     }  
    }  
  
    void schedule(int remainingjobs, int jobendtime, int coolofftime, queue<std::pair<int,int>>& future ){  
        if(remainingjobs > 0){  
            int next = jobendtime + coolofftime;  
            future.push(std::make_pair(next,remainingjobs));  
        }  
    }  
  
public:  
    int leastInterval(vector<char>& tasks, int n) {  
        vector<int> heapschedule = getFrequencies(tasks);  
        std::make_heap(heapschedule.begin(),heapschedule.end());  
        queue<std::pair<int,int>> future;  
        int time = 0;  
        while(!heapschedule.empty() || !future.empty()){  
            /*schedules to now*/  
            schedule(future,heapschedule,time);  
            if(!heapschedule.empty()){  
                int cf = heapschedule[0];  
                /*pushes it to the last*/  
                std::pop_heap(heapschedule.begin(),heapschedule.end());  
                /*remove it*/  
                heapschedule.pop_back();  
                /*schedules into future*/  
                schedule(cf-1,time+1,n,future);  
            }  
            time++;  
        }  
        return time;  
    }  
};  
  
void test_scheduler(){  
    vector<char> tasks = {'A','A','A','A','A','A','B','C','D','E','F','G'};  
    Solution s;  
    cout << s.leastInterval(tasks,2) << endl;  
}
```

# 🧠 Ideas about Problem

# 🔗 Related Applications

