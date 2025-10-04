# Day 1 Problem 1 : Majority Element  
**Platform:** LeetCode  
**Difficulty:** Easy  
**Topic:** Arrays 
- [LeetCode Problem: Majority Element](https://leetcode.com/problems/majority-element/description/)

##  Problem Statement  
Given an array `nums` of size `n`, return the **majority element**.  
The majority element is the element that appears **more than ⌊n / 2⌋ times**.  
You may assume that the majority element always exists in the array.  
Constraints:  
->n == nums.length  
->1 <= n <= 5 * 104  
->-109 <= nums[i] <= 109

## Brute Force Approach:
### Idea: 
The Brute Force approach consists of comparing every element of the array with all the other elements of the array using the method of nested loops. As the index of the inside loop increases we check whether it is equal to the element of the outer loop, if equal we increase our count variable by 1. At the end we check whether our count variable is greater than half the length of our array and return the majority element.
(since the assumption is that the majority element always exists in the array, we will always return an integer, the variation for this problem is discussed below.)

### Code:
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int len=nums.size();
        for (int val:nums){
            int count=0;
            for (int ele:nums){
                if (ele==val) count++;
            }
            if (count>len/2) return val;
        }
    }
};

### complexity Analysis
**Time Complexity**:O(n²)  
**Space Complexity**:O(1)
Since the time complexity is greater than the constraint, this code will give TLE.

## Better Approach:

### Idea:  
The Logic is to sort the array before finding the majority element, as it will bunch the same numbers together causing our majority element to appear multiple times in consecutive successions.

### Code:
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int len=nums.size();
        sort(nums.begin(), nums.end());
        int count=1, ind=nums[0];
        for (int i=1; i<len; i++){
            if (nums[i]==nums[i-1]) count++;
            else count=1, ind=nums[i];
            if (count>len/2) return ind;
        }
        return ind;
    }
};

### Complexity Analysis
**Time Complexity**:O(nlogn)  
**Space Complexity**:O(1)
This code will be accepted as the solution.

## Optimal Approach (Moore's Voting):

### Idea:
Here we will track the frequency of every element, as the element changes the frequency will revert back to 0. Causing the element with the maximum frequency to be returned.

### code:
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int len=nums.size();
        int count=0, ind=0;
        for (int i=0; i<len; i++){
            if (count==0) ind=nums[i];
            if (ind==nums[i]) count++;
            else count--;
        }
        return ind;
    }
};

### Complexity Analysis
**Time Complexity**:O(n)  
**Space Complexity**:O(1)

## Variation Approach:

### Idea:
Since the question comes with the assumption that the majority element always exists in the array, an edge case where no majority element exists, should be handled.

### Code:
int mj(vector<int>& l){
    int n=l.size();
    int f=0, a=0;
    for (int i=0; i<n; i++){
        if (f==0) a=l[i];
        if (a==l[i]) f++;
        else f--;
    }
    int c=0;
    for (int e:l){
        if (e==a) c++;
    }
    if (c>(n/2)) return a;
    else return -1;
}

### Complexity Analysis:
**Time Complexity**:O(n)  
**Space Complexity**:O(1)







