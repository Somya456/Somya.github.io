# Day 1 Problem 2 : Pow(x,n)
**Platform**: Leetcode  
**Difficulty**:Medium  
**Topics**: Math, Recursion  
- [Leetcode Problem: Pow(x,n)] (https://leetcode.com/problems/powx-n/description/)

## Problem Statement
Implement pow(x, n), which calculates x raised to the power n (i.e., $x^n$).  
Constraints:  
->-100.0 < x < 100.0  
->-231 <= n <= 231-1  
->n is an integer. Either x is not zero or n > 0.  
->-104 <= xn <= 104

## Approach:

### Idea:
Compute $x^n$ using binary exponentiation, where we will apply a loop on the binary form of the exponent.
Here we take a long variable binform and give it the value of n and a double variable a initialised with 1, while binform is greater than 0 if for every time on dividing it by 2 the remainder equals 1, we multiply a by x, as well square the x and halve binform. Lastly returning a.

### Code:
class Solution {
public:
    double myPow(double x, int n) {
      long binform=n;
      double a=1;
      if (n<0) x=1/x, binform=-binform;
      while (binform>0){
        if(binform%2==1) a*=x;
        x*=x, binform/=2;
      }  
      return a;
    }
};

### Complexity Analysis:
**Time Complexity**:O(logn)  
**Space Complexity**: O(1)

### Covering other edge cases:  
-**if n is 0 or x is 1** : return 1  
-**if x is 0** : return 0  
-**if x is -1 and n is even** : return 1  
-**if x is -1 and n is odd** : return -1

### Code:
class Solution {
public:
    double myPow(double x, int n) {
        if (n==0 || x==1) return 1.0;
        if (x==0) return 0.0;
        if (x==-1 && n%2==0) return 1.0;
        if (x==-1 && n%2!=0) return -1.0;
        long binform=n;
        double a=1;
        if (n<0) x=1/x, binform=-binform;
        while (binform>0){
            if (binform%2==1) a*=x;
            x*=x, binform/=2;
        }
        return a;
    }
};
