# Distinct

Write a function

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers, returns the number of distinct values in array A.

For example, given array A consisting of six elements such that:

 A[0] = 2    A[1] = 1    A[2] = 1
 A[3] = 2    A[4] = 3    A[5] = 1
the function should return 3, because there are 3 distinct values appearing in array A, namely 1, 2 and 3.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
each element of array A is an integer within the range [−1,000,000..1,000,000].

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
        if (A.length == 0) {
            return 0;
        }
        
        Arrays.sort(A);
        
        int count = 1;
        
        for (int i = 1; i < A.length; ++i) {
            
            if (A[i] != A[i - 1]) {
                ++count;
            }
        }
        
        return count;
    }
}
```

## Python Solution

```python
def solution(A):
    
    if len(A) == 0:
        return 0
    
    A = sorted(A)
        
    count = 1
    
    for i in range(1, len(A)):
        
        if A[i] != A[i - 1]:
            count += 1
    
    return count
```

# Max Product of Three

A non-empty array A consisting of N integers is given. The product of triplet (P, Q, R) equates to A[P] * A[Q] * A[R] (0 ≤ P < Q < R < N).

For example, array A such that:

  A[0] = -3
  A[1] = 1
  A[2] = 2
  A[3] = -2
  A[4] = 5
  A[5] = 6
contains the following example triplets:

(0, 1, 2), product is −3 * 1 * 2 = −6
(1, 2, 4), product is 1 * 2 * 5 = 10
(2, 4, 5), product is 2 * 5 * 6 = 60
Your goal is to find the maximal product of any triplet.

Write a function:

class Solution { public int solution(int[] A); }

that, given a non-empty array A, returns the value of the maximal product of any triplet.

For example, given array A such that:

  A[0] = -3
  A[1] = 1
  A[2] = 2
  A[3] = -2
  A[4] = 5
  A[5] = 6
the function should return 60, as the product of triplet (2, 4, 5) is maximal.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [3..100,000];
each element of array A is an integer within the range [−1,000..1,000].

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
        Arrays.sort(A);
        
        int firstMax = A[0] * A[1] * A[A.length - 1];
        int lastMax = A[A.length - 3] * A[A.length - 2] * A[A.length -1];
        
        return firstMax > lastMax ? firstMax : lastMax;
    }
}
```

## Python Solution

```python
def solution(A):
    
    A = sorted(A)
    
    firstMax = A[0] * A[1] * A[len(A) - 1]
    lastMax = A[len(A) - 3] * A[len(A) - 2] * A[len(A) - 1]
    
    return firstMax if firstMax > lastMax else lastMax
```

# Triangle

An array A consisting of N integers is given. A triplet (P, Q, R) is triangular if 0 ≤ P < Q < R < N and:

A[P] + A[Q] > A[R],
A[Q] + A[R] > A[P],
A[R] + A[P] > A[Q].
For example, consider array A such that:

  A[0] = 10    A[1] = 2    A[2] = 5
  A[3] = 1     A[4] = 8    A[5] = 20
Triplet (0, 2, 4) is triangular.

Write a function:

class Solution { public int solution(int[] A); }

that, given an array A consisting of N integers, returns 1 if there exists a triangular triplet for this array and returns 0 otherwise.

For example, given array A such that:

  A[0] = 10    A[1] = 2    A[2] = 5
  A[3] = 1     A[4] = 8    A[5] = 20
the function should return 1, as explained above. Given array A such that:

  A[0] = 10    A[1] = 50    A[2] = 5
  A[3] = 1
the function should return 0.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [0..100,000];
each element of array A is an integer within the range [−2,147,483,648..2,147,483,647].

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
        if (A.length < 3) {
            return 0;
        }
        
        Arrays.sort(A);
        
        for (int i = 0; i < A.length - 2; ++i) {
            
            if (A[i] + A[i + 1] > A[i + 2]) {
                return 1;
            }
        }
        
        return 0;
    }
}
```

## Python Solution

```python
def solution(A):
    
    if len(A) < 3:
        return 0
    
    A.sort() 
      
    for i in range(len(A) - 2):
        
        if A[i] + A[i + 1] > A[i + 2]:
            return 1
            
    return 0
```

