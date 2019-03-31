# Frog Jump

A small frog wants to get to the other side of the road. The frog is currently located at position X and wants to get to a position greater than or equal to Y. The small frog always jumps a fixed distance, D.

Count the minimal number of jumps that the small frog must perform to reach its target.

Write a function:

__class Solution { public int solution(int X, int Y, int D); }__

that, given three integers X, Y and D, returns the minimal number of jumps from position X to a position equal to or greater than Y.

For example, given:  

  X = 10  
  Y = 85  
  D = 30  

the function should return 3, because the frog will be positioned as follows:

after the first jump, at position 10 + 30 = 40  
after the second jump, at position 10 + 30 + 30 = 70  
after the third jump, at position 10 + 30 + 30 + 30 = 100  

Write an efficient algorithm for the following assumptions:

X, Y and D are integers within the range [1..1,000,000,000];
X ≤ Y.

## Java Solution

```java
class Solution {
    public int solution(int X, int Y, int D) {
        
        return (int) Math.ceil((Y - X) / (double) D);
    }
}
```

## Python Solution

```python
import math

def solution(X, Y, D):
    
    return math.ceil((Y - X) / D)
```

# Perm Missing Elem

An array A consisting of N different integers is given. The array contains integers in the range [1..(N + 1)], which means that exactly one element is missing.

Your goal is to find that missing element.

Write a function:

__class Solution { public int solution(int[] A); }__

that, given an array A, returns the value of the missing element.

For example, given array A such that:

  A[0] = 2  
  A[1] = 3  
  A[2] = 1  
  A[3] = 5  

the function should return 4, as it is the missing element.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
the elements of A are all distinct;
each element of array A is an integer within the range [1..(N + 1)].

## Java Solution

```java
import java.util.*;

class Solution {
    public int solution(int[] A) {

        if (A.length == 0) {
            return 1;
        }

        Arrays.sort(A);

        for (int i = 0; i < A.length - 1; ++i) {
            
            if (A[i + 1] - A[i] != 1) {
                return A[i] + 1;
            }
        }
        
        return A[0] == 1 ? A.length + 1 : 1;
    }
}
```

## Python Solution

```python
def solution(A):
    
    if len(A) == 0:
        return 1
        
    A = sorted(A)
        
    for i in range(0, len(A) - 1):    
        
        if A[i + 1] - A[i] != 1:
            return A[i] + 1
        
    return len(A) + 1 if A[0] == 1 else 1; 
```



# Tape Equilibrium

A non-empty array A consisting of N integers is given. Array A represents numbers on a tape.

Any integer P, such that 0 < P < N, splits this tape into two non-empty parts: A[0], A[1], ..., A[P − 1] and A[P], A[P + 1], ..., A[N − 1].

The *difference* between the two parts is the value of: |(A[0] + A[1] + ... + A[P − 1]) − (A[P] + A[P + 1] + ... + A[N − 1])|

In other words, it is the absolute difference between the sum of the first part and the sum of the second part.

For example, consider array A such that:

* A[0] = 3  
*  A[1] = 1  
*  A[2] = 2  
*  A[3] = 4   
* A[4] = 3

We can split this tape in four places:

* P = 1, difference = |3 − 10| = 7 
* P = 2, difference = |4 − 9| = 5 
* P = 3, difference = |6 − 7| = 1 
* P = 4, difference = |10 − 3| = 7 

Write a function:

__class Solution { public int solution(int[] A); }__

that, given a non-empty array A of N integers, returns the minimal difference that can be achieved.

For example, given:

* A[0] = 3  
*  A[1] = 1  
*  A[2] = 2   
* A[3] = 4   
* A[4] = 3

the function should return 1, as explained above.

Write an **efficient** algorithm for the following assumptions:

* N is an integer within the range [2..100,000];

* each element of array A is an integer within the range [−1,000..1,000].

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
      	int sum = 0;
        
        for (int num : A) {
            sum += num;
        }
        
        int leftSum = 0;
        int difference = Integer.MAX_VALUE;
        
        for (int i = 0; i < A.length -1; ++i) {
            
            leftSum += A[i];
            
            int rightSum = sum - leftSum;
            int currentDifference = Math.abs(leftSum - rightSum);
          
            if (currentDifference < difference) {
                difference = currentDifference;
            }
        }
        
        return difference;
    }
}
```



## Python Solution

```python
import sys

def solution(A):
   
    sum = 0
   
    for num in A:
        sum += num
        
    leftSum = 0
    difference = sys.maxsize
    
    for i in range(0, len(A) - 1):
        
        leftSum += A[i]
        rightSum = sum - leftSum
        currentDifference = abs(leftSum - rightSum)
        
        if (currentDifference < difference):
            difference = currentDifference
    
    return difference
```

