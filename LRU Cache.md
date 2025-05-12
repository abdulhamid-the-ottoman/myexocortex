---
created:
  - 2023-07-01 15:38
share: true
---

up::

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
>- Design a data structure that follows the constraints of a **[Least Recently Used (LRU) cache](https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU)**.
> 
> Implement the `LRUCache` class:
> 
> - `LRUCache(int capacity)` Initialize the LRU cache with **positive** size `capacity`.
> - `int get(int key)` Return the value of the `key` if the key exists, otherwise return `-1`.
> - `void put(int key, int value)` Update the value of the `key` if the `key` exists. Otherwise, add the `key-value`pair to the cache. If the number of keys exceeds the `capacity` from this operation, **evict** the least recently used key.
> 
> The functions `get` and `put` must each run in `O(1)` average time complexity.
> 
> **Example 1:**
> 
> **Input**
> ["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
> \[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
> **Output**
> [null, null, null, 1, null, -1, null, -1, 3, 4]
> 
> **Explanation**
> LRUCache lRUCache = new LRUCache(2);
> lRUCache.put(1, 1); // cache is {1=1}
> lRUCache.put(2, 2); // cache is {1=1, 2=2}
> lRUCache.get(1);    // return 1
> lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
> lRUCache.get(2);    // returns -1 (not found)
> lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
> lRUCache.get(1);    // return -1 (not found)
> lRUCache.get(3);    // return 3
> lRUCache.get(4);    // return 4
> 
> **Constraints:**
> 
> - `1 <= capacity <= 3000`
> - `0 <= key <= 104`
> - `0 <= value <= 105`
> - At most `2 * 105` calls will be made to `get` and `put`.


## 🔑 **Key Points of Understanding**
- We can use 2 data structures to implement an LRU cache.
	- Doubly Linked Dequeue: 
		- The max size of the queue will be equal to the total number of frames available (cache size).
		- The most recently used pages will be related to the front.
		- The least recently used pages will be related to the back
	- Hash-map:
		- Page numbers as key, and the corresponding dequeue node as value.
- How?
	- When a page is referenced, the required page may be in the memory.
		- If it is in the memory, we need to detach the node of list and bring it to front of the queue.
		- If it is not in the memory, we bring that and add it to the front of the queue and update the corresponding hashmap entry.
	- If all the frames are full, we remove a node from the rear of the queue and update the hashmap and add the new node to the front of the queue.
# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications

