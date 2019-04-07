# Perm Check

A non-empty array A consisting of N integers is given.

A *permutation* is a sequence containing each element from 1 to N once, and only once.

For example, array A such that:

* A[0] = 4    
*  A[1] = 1    
*  A[2] = 3    
*  A[3] = 2

is a permutation, but array A such that:

*  A[0] = 4    
*  A[1] = 1    
*  A[2] = 3

is not a permutation, because value 2 is missing.

The goal is to check whether array A is a permutation.

Write a function:

__class Solution { public int solution(int[] A); }__

that, given an array A, returns 1 if array A is a permutation and 0 if it is not.

For example, given array A such that:

* A[0] = 4    
*  A[1] = 1     
* A[2] = 3    
*  A[3] = 2

the function should return 1.

Given array A such that:

*  A[0] = 4    
*  A[1] = 1    
*  A[2] = 3

the function should return 0.

Write an **efficient** algorithm for the following assumptions:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [1..1,000,000,000].

## Java Solution

```java
import java.util.*;

class Solution {
    public int solution(int[] A) {

        Arrays.sort(A);
        
        for (int i = 0; i < A.length; ++i) {
            
            if (A[i] != i + 1) {
                return 0;
            }
        }
     
        return 1;   
    }
}
```

## Python Solution

```python
def solution(A):
    
    A = sorted(A)
    
    for i in range(0, len(A)):
        
        if A[i] != i + 1:
            return 0
    
    return 1
```

# Frog River One

A small frog wants to get to the other side of a river. The frog is initially located on one bank of the river (position 0) and wants to get to the opposite bank (position X+1). Leaves fall from a tree onto the surface of the river.

You are given an array A consisting of N integers representing the falling leaves. A[K] represents the position where one leaf falls at time K, measured in seconds.

The goal is to find the earliest time when the frog can jump to the other side of the river. The frog can cross only when leaves appear at every position across the river from 1 to X (that is, we want to find the earliest moment when all the positions from 1 to X are covered by leaves). You may assume that the speed of the current in the river is negligibly small, i.e. the leaves do not change their positions once they fall in the river.

For example, you are given integer X = 5 and array A such that:

  A[0] = 1
  A[1] = 3
  A[2] = 1
  A[3] = 4
  A[4] = 2
  A[5] = 3
  A[6] = 5
  A[7] = 4

In second 6, a leaf falls into position 5. This is the earliest time when leaves appear in every position across the river.

Write a function:

class Solution { public int solution(int X, int[] A); }

that, given a non-empty array A consisting of N integers and integer X, returns the earliest time when the frog can jump to the other side of the river.

If the frog is never able to jump to the other side of the river, the function should return −1.

For example, given X = 5 and array A such that:

  A[0] = 1
  A[1] = 3
  A[2] = 1
  A[3] = 4
  A[4] = 2
  A[5] = 3
  A[6] = 5
  A[7] = 4

the function should return 6, as explained above.

Write an efficient algorithm for the following assumptions:

* N and X are integers within the range [1..100,000];
* each element of array A is an integer within the range [1..X].

## Java Solution

```java
import java.util.*;

class Solution {
    public int solution(int X, int[] A) {
        
        Set<Integer> leaves = new HashSet<>();
        
        for (int i = 0; i < A.length; ++i) {
            
            if (A[i] <= X) {
                leaves.add(A[i]);
            }
            
            if (leaves.size() == X) {
                return i;
            }
        }
        
        return -1;
    }
}
```

## Python Solution

```python
def solution(X, A):
    
    leaves = set()
    
    for i in range(0, len(A)):
        
        if A[i] <= X:
            leaves.add(A[i])
            
        if len(leaves) == X:
            return i
            
    return -1
```

# Max Counters

You are given N counters, initially set to 0, and you have two possible operations on them:

increase(X) − counter X is increased by 1,
max counter − all counters are set to the maximum value of any counter.
A non-empty array A of M integers is given. This array represents consecutive operations:

if A[K] = X, such that 1 ≤ X ≤ N, then operation K is increase(X),
if A[K] = N + 1 then operation K is max counter.
For example, given integer N = 5 and array A such that:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4
the values of the counters after each consecutive operation will be:

    (0, 0, 1, 0, 0)
    (0, 0, 1, 1, 0)
    (0, 0, 1, 2, 0)
    (2, 2, 2, 2, 2)
    (3, 2, 2, 2, 2)
    (3, 2, 2, 3, 2)
    (3, 2, 2, 4, 2)
The goal is to calculate the value of every counter after all operations.

Write a function:

class Solution { public int[] solution(int N, int[] A); }

that, given an integer N and a non-empty array A consisting of M integers, returns a sequence of integers representing the values of the counters.

Result array should be returned as an array of integers.

For example, given:

    A[0] = 3
    A[1] = 4
    A[2] = 4
    A[3] = 6
    A[4] = 1
    A[5] = 4
    A[6] = 4
the function should return [3, 2, 2, 4, 2], as explained above.

Write an efficient algorithm for the following assumptions:

N and M are integers within the range [1..100,000];
each element of array A is an integer within the range [1..N + 1].

## Java Solution

```java
class Solution {
    public int[] solution(int N, int[] A) {

        int[] counters = new int[N];
        int maxCounter = 0;
        int currentMax = 0;

        for (int i : A) {

            if (i >= 1 && i <= N) {
                
                if (maxCounter > counters[i - 1]) {
                    counters[i - 1] = maxCounter;
                }
            
                counters[i - 1] += 1;
            
                if (currentMax < counters[i - 1]) {
                    currentMax = counters[i - 1];
                }
                
            } else if (i == N + 1) {
                maxCounter = currentMax;
            }
        }
        
        for (int i = 0; i < counters.length; ++i) {
            if (counters[i] < maxCounter) {
                counters[i] = maxCounter;
            }
        }
        
        return counters;       
    }
}
```

## Python Solution

```python
def solution(N, A):

    counters = [0] * N;
    current_max = 0;
    max_counter = 0;
    
    for op in A:
        
        if op >= 1 and op <= N:
            
            if max_counter > counters[op - 1]:
                counters[op - 1] = max_counter
                
            counters[op - 1] += 1
            
            if current_max < counters[op - 1]:
                current_max = counters[op - 1]
        
        elif op == N + 1:
            
            if current_max > max_counter:
                max_counter = current_max
    
    for i in range(0, len(counters)):
        
        if counters[i] < max_counter:
            counters[i] = max_counter;
    
    return counters
```



# Missing Integer

Write a function:

class Solution { public int solution(int[] A); }

that, given an array A of N integers, returns the smallest positive integer (greater than 0) that does not occur in A.

For example, given A = [1, 3, 6, 4, 1, 2], the function should return 5.

Given A = [1, 2, 3], the function should return 4.

Given A = [−1, −3], the function should return 1.

Write an efficient algorithm for the following assumptions:

* N is an integer within the range [1..100,000];
* each element of array A is an integer within the range [−1,000,000..1,000,000].

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
        Arrays.sort(A);
        
        if (A[A.length - 1] <= 0) {
            return 1;
        }
        
        int missingNum = 1;
        
        for (int i = 0; i < A.length; ++i) {

            if (A[i] > 0) {
                
                if (A[i] != missingNum) {
                    break;
                }
            
                if (A[i] == missingNum) {
                
                    if (i == A.length - 1) {
                        ++missingNum;
                        break;
                    }
                
                    if (A[i] != A[i + 1]) {
                        ++missingNum;
                    }
                } 
            }
        }
        
        return missingNum;
    }
}
```

## Python Solution

```python
def solution(A):
    
    A = sorted(A)
    
    if A[len(A) - 1] <= 0:
        return 1
    
    missing_num = 1
    
    for i in range(0, len(A)):
        
        if A[i] < 1:
            continue
        
        if A[i] != missing_num:
            break
        
        if A[i] == missing_num:
            
            if i == len(A) - 1:
                missing_num += 1
                break
                
            if A[i] != A[i + 1]:
                missing_num += 1
                
    return missing_num
```

