---
created:
  - 2023-07-11 20:30
share: true
---

up::[Heaps](NeetCode%20Index.md#^c810f8)

# ❗ Information
Related to:: 
Tags:: 

___
# 🌍 Problem Definition

> [!QUESTION] Problem
> Design a simplified version of Twitter where users can post tweets, follow/unfollow another user, and is able to see the `10` most recent tweets in the user's news feed.
> 
> Implement the `Twitter` class:
> 
> - `Twitter()` Initializes your twitter object.
> - `void postTweet(int userId, int tweetId)` Composes a new tweet with ID `tweetId` by the user `userId`. Each call to this function will be made with a unique `tweetId`.
> - `List<Integer> getNewsFeed(int userId)` Retrieves the `10` most recent tweet IDs in the user's news feed. Each item in the news feed must be posted by users who the user followed or by the user themself. Tweets must be **ordered from most recent to least recent**.
> - `void follow(int followerId, int followeeId)` The user with ID `followerId` started following the user with ID `followeeId`.
> - `void unfollow(int followerId, int followeeId)` The user with ID `followerId` started unfollowing the user with ID `followeeId`.
> 
> ![Pasted image 20230711203312.png](./40-referenceVAULTS/Resource%20Library/Images/Pasted%20image%2020230711203312.png)
> 
> **Constraints:**
> 
> - `1 <= userId, followerId, followeeId <= 500`
> - `0 <= tweetId <= 104`
> - All the tweets have **unique** IDs.
> - At most `3 * 104` calls will be made to `postTweet`, `getNewsFeed`, `follow`, and `unfollow`.




## 🔑 **Key Points of Understanding**

# 🔍 Solutions

# 🧠 Ideas about Problem

# 🔗 Related Applications

