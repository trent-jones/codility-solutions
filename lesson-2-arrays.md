
# Cyclic Rotation

An array A consisting of N integers is given. Rotation of the array means that each element is shifted right by one index, and the last element of the array is moved to the first place. For example, the rotation of array A = [3, 8, 9, 7, 6] is [6, 3, 8, 9, 7] (elements are shifted right by one index and 6 is moved to the first place).

The goal is to rotate array A K times; that is, each element of A will be shifted to the right K times.

Write a function:

__class Solution { public int[] solution(int[] A, int K); }__

that, given an array A consisting of N integers and an integer K, returns the array A rotated K times.

For example, given

    A = [3, 8, 9, 7, 6]
    K = 3
the function should return [9, 7, 6, 3, 8]. Three rotations were made:

    [3, 8, 9, 7, 6] -> [6, 3, 8, 9, 7]
    [6, 3, 8, 9, 7] -> [7, 6, 3, 8, 9]
    [7, 6, 3, 8, 9] -> [9, 7, 6, 3, 8]
For another example, given

    A = [0, 0, 0]
    K = 1
the function should return [0, 0, 0]

Given

    A = [1, 2, 3, 4]
    K = 4
the function should return [1, 2, 3, 4]

Assume that:

N and K are integers within the range [0..100];
each element of array A is an integer within the range [−1,000..1,000].

## Java Solution

```java
class Solution {
    public int[] solution(int[] A, int K) {
        
        if (A.length == 0) {
            return A;
        }
        
        int[] B = new int[A.length];
        int shiftAmount = K % A.length;
        
        for(int i = 0; i < A.length; ++i) {
            B[(shiftAmount + i) % A.length] = A[i];
        }
        
        return B;
    }
}
```

## Python Solution

```python
def solution(A, K):
    
    if len(A) == 0:
        return []
    
    shift_amount = K % len(A)
    B = []

    [B.insert((i + shift_amount) % len(A), val) for i, val in enumerate(A)]

    # or without list comprehension
    # for i, val in enumerate(A):
    #     B.insert((i + shift_amount) % len(A), val)
    
    return B
```

## Go Solution

```go
func Solution(A []int, K int) []int {
    
    if len(A) == 0 {
        return A
    }
    
    shiftAmount := K % len(A)
    B := make([]int, len(A))
    
    for i, val := range A {
        B[(i + shiftAmount) % len(A)] = val
    }
    
    return B
}
```

# Odd Occurrences In Array

A non-empty array A consisting of N integers is given. The array contains an odd number of elements, and each element of the array can be paired with another element that has the same value, except for one element that is left unpaired.

For example, in array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9  
  A[3] = 3  A[4] = 9  A[5] = 7  
  A[6] = 9  
  
the elements at indexes 0 and 2 have value 9,  
the elements at indexes 1 and 3 have value 3,  
the elements at indexes 4 and 6 have value 9,  
the element at index 5 has value 7 and is unpaired.  

Write a function:

__class Solution { public int solution(int[] A); }__

that, given an array A consisting of N integers fulfilling the above conditions, returns the value of the unpaired element.

For example, given array A such that:

  A[0] = 9  A[1] = 3  A[2] = 9  
  A[3] = 3  A[4] = 9  A[5] = 7  
  A[6] = 9  
  
the function should return 7, as explained in the example above.

Write an efficient algorithm for the following assumptions:

N is an odd integer within the range [1..1,000,000];
each element of array A is an integer within the range [1..1,000,000,000];
all but one of the values in A occur an even number of times.

## Java Solution

```java
class Solution {
    public int solution(int[] A) {
        
        // Java 8 Arrays.sort is a dual-pivot quicksort with time complexity O(n log(n))
        Arrays.sort(A);

        for (int i = 0; i < A.length - 2; i = i + 2) {
            
            if (A[i] != A[i + 1]) {
                
                if (A[i + 1] != A[i + 2]) {
                    return A[i + 1];
                } else {
                    return A[i];
                }
            }
        }
        
        return A[A.length - 1];
    }
}
```

## Python Solution

```python
def solution(A):
    
    A = sorted(A)

    for i in range(0, len(A) - 2, 2):
        
        if A[i] != A[i + 1]:
            return A[i + 1] if A[i + 1] != A[i + 2] else A[i]
    
    return A[len(A) - 1]
```

## Go Solution

```go
func Solution(A []int) int {
    
    sort.Ints(A)
    
    for i := 0; i < len(A) - 2; i = i + 2 {
        
        if A[i] != A[i + 1] {
            
            if A[i + 1] != A[i + 2] {
                return A[i + 1]
            } else {
                return A[i]
            }
        }
    }
    
    return A[len(A) - 1]
}
```