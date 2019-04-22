# Passing Cars

A non-empty array A consisting of N integers is given. The consecutive elements of array A represent consecutive cars on a road.

Array A contains only 0s and/or 1s:

0 represents a car traveling east,
1 represents a car traveling west.
The goal is to count passing cars. We say that a pair of cars (P, Q), where 0 ≤ P < Q < N, is passing when P is traveling to the east and Q is traveling to the west.

For example, consider array A such that:

  A[0] = 0
  A[1] = 1
  A[2] = 0
  A[3] = 1
  A[4] = 1

We have five pairs of passing cars: (0, 1), (0, 3), (0, 4), (2, 3), (2, 4).

Write a function:

​	__class Solution { public int solution(int[] A); }__

that, given a non-empty array A of N integers, returns the number of pairs of passing cars.

The function should return −1 if the number of pairs of passing cars exceeds 1,000,000,000.

For example, given:

  A[0] = 0
  A[1] = 1
  A[2] = 0
  A[3] = 1
  A[4] = 1

the function should return 5, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
each element of array A is an integer that can have one of the following values: 0, 1.

## Java Solution

```java
import java.util.*;

class Solution {
  
    private int[] getPrefixSum(int[] A) {
        
        int[] prefixSum = new int[A.length];
        
        prefixSum[0] = A[0];
        
        for (int i = 1; i < A.length; ++i) {
            prefixSum[i] = prefixSum[i - 1] + A[i];
        }
      
        return prefixSum;
    }    
    
    public int solution(int[] A) {
        
        int[] prefixSum = this.getPrefixSum(A);
        int passingCars = 0;
 
        for (int i = 0; i < A.length; ++i) {
            
            if (A[i] == 0) {
                passingCars += prefixSum[A.length - 1] - prefixSum[i];
            }
        }

        return Math.abs(passingCars) > 1000000000 ? -1 : passingCars;
    }
}
```

## Python Solution

```python
def getPrefixSum(A):
    
    prefixSum = [0] * len(A)
    prefixSum[0] = A[0]

    for i in range (1, len(A)):
        prefixSum[i] += prefixSum[i - 1] + A[i]
    
    return prefixSum


def solution(A):

    prefixSum = getPrefixSum(A)
    passingCars = 0
    
    for i in range (len(A)):
        
        if A[i] == 0:
            passingCars += prefixSum[len(A) - 1] - prefixSum[i]
    
    return -1 if abs(passingCars) > 1000000000 else passingCars
```

## Go Solution

```go
func getPrefixSum(A []int) []int {
    
    prefixSum := make([]int, len(A))
    prefixSum[0] = A[0]
    
    for i := 1; i < len(A); i++ {
        prefixSum[i] = prefixSum[i - 1] + A[i]
    }

    return prefixSum
}

func abs(x int) int {
    
    if x < 0 {
        return -x
    }
    
    return x
}

func Solution(A []int) int {

    prefixSum := getPrefixSum(A)
    passingCars := 0

    for i := 0; i < len(A); i++ {
        
        if A[i] == 0 {
            passingCars += prefixSum[len(A) - 1] - prefixSum[i]
        }
    }
    
    if abs(passingCars) > 1000000000 {
        return -1
    } else {
        return passingCars
    }
}
```

# Genomic Range Query

A DNA sequence can be represented as a string consisting of the letters A, C, G and T, which correspond to the types of successive nucleotides in the sequence. Each nucleotide has an impact factor, which is an integer. Nucleotides of types A, C, G and T have impact factors of 1, 2, 3 and 4, respectively. You are going to answer several queries of the form: What is the minimal impact factor of nucleotides contained in a particular part of the given DNA sequence?

The DNA sequence is given as a non-empty string S = S[0]S[1]...S[N-1] consisting of N characters. There are M queries, which are given in non-empty arrays P and Q, each consisting of M integers. The K-th query (0 ≤ K < M) requires you to find the minimal impact factor of nucleotides contained in the DNA sequence between positions P[K] and Q[K] (inclusive).

For example, consider string S = CAGCCTA and arrays P, Q such that:

    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6
The answers to these M = 3 queries are as follows:

The part of the DNA between positions 2 and 4 contains nucleotides G and C (twice), whose impact factors are 3 and 2 respectively, so the answer is 2.
The part between positions 5 and 5 contains a single nucleotide T, whose impact factor is 4, so the answer is 4.
The part between positions 0 and 6 (the whole string) contains all nucleotides, in particular nucleotide A whose impact factor is 1, so the answer is 1.
Write a function:

class Solution { public int[] solution(String S, int[] P, int[] Q); }

that, given a non-empty string S consisting of N characters and two non-empty arrays P and Q consisting of M integers, returns an array consisting of M integers specifying the consecutive answers to all queries.

Result array should be returned as an array of integers.

For example, given the string S = CAGCCTA and arrays P, Q such that:

    P[0] = 2    Q[0] = 4
    P[1] = 5    Q[1] = 5
    P[2] = 0    Q[2] = 6
the function should return the values [2, 4, 1], as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [1..100,000];
M is an integer within the range [1..50,000];
each element of arrays P, Q is an integer within the range [0..N − 1];
P[K] ≤ Q[K], where 0 ≤ K < M;
string S consists only of upper-case English letters A, C, G, T.



## Java Solution

```java
class Solution {

    private static final Character A = 'A';
    private static final Character C = 'C';
    private static final Character G = 'G';
    private static final Character T = 'T';
    
    private static final Map<Character, Integer> IMPACT_FACTORS = new HashMap<Character, Integer>();
    
    {
        IMPACT_FACTORS.put(A, 1);
        IMPACT_FACTORS.put(C, 2);
        IMPACT_FACTORS.put(G, 3);
        IMPACT_FACTORS.put(T, 4);
    };
    
    public int[] solution(String S, int[] P, int[] Q) {
    
        Map<Character, int[]> counters = new HashMap<>();
        counters.put(A, new int[S.length() + 1]);
        counters.put(C, new int[S.length() + 1]);
        counters.put(G, new int[S.length() + 1]);
        counters.put(T, new int[S.length() + 1]);
        
        char[] sequence = S.toCharArray();

        for (int i = 0; i < sequence.length; ++i) {        
        
            ++counters.get(sequence[i])[i + 1];

            counters.get(A)[i + 1] += counters.get(A)[i];
            counters.get(C)[i + 1] += counters.get(C)[i];
            counters.get(G)[i + 1] += counters.get(G)[i];
            counters.get(T)[i + 1] += counters.get(T)[i];
        }

        int[] minimalImpactFactors = new int[P.length];
    
        for (int i = 0; i < P.length; ++i) {
            
            int start = P[i];
            int end = Q[i] + 1;

            if (start == end) {
                minimalImpactFactors[i] = IMPACT_FACTORS.get(sequence[start]);
            } else if (counters.get(A)[end] > counters.get(A)[start]) {
                minimalImpactFactors[i] = IMPACT_FACTORS.get(A);
            } else if (counters.get(C)[end] > counters.get(C)[start]) {
                minimalImpactFactors[i] = IMPACT_FACTORS.get(C);
            } else if (counters.get(G)[end] > counters.get(G)[start]) {
                minimalImpactFactors[i] = IMPACT_FACTORS.get(G);
            } else {
                minimalImpactFactors[i] = IMPACT_FACTORS.get(T);
            }
        }
    
        return minimalImpactFactors;
    }
}
```

## Python Solution

```python
A = 'A'
C = 'C'
G = 'G'
T = 'T'

IMPACT_FACTORS = {
    A: 1,
    C: 2,
    G: 3,
    T: 4
}

def solution(S, P, Q):
    
    a_counter = [0] * (len(S) + 1)
    c_counter = [0] * (len(S) + 1)
    g_counter = [0] * (len(S) + 1)
    t_counter = [0] * (len(S) + 1)
    
    minImpactFactors = [0] * len(P)
    
    for i in range(0, len(S)):
        
        if S[i] == A:
            a_counter[i + 1] += 1
        elif S[i] == C:
            c_counter[i + 1] += 1
        elif S[i] == G:
            g_counter[i + 1] += 1
        else:
            t_counter[i + 1] += 1
            
        a_counter[i + 1] += a_counter[i]
        c_counter[i + 1] += c_counter[i]
        g_counter[i + 1] += g_counter[i]
        t_counter[i + 1] += t_counter[i]
    
    for i in range(0, len(P)):
        
        start = P[i]
        end = Q[i] + 1
        
        if a_counter[end] > a_counter[start]:
            minImpactFactors[i] = IMPACT_FACTORS[A]
        elif c_counter[end] > c_counter[start]:
            minImpactFactors[i] = IMPACT_FACTORS[C]
        elif g_counter[end] > g_counter[start]:
            minImpactFactors[i] = IMPACT_FACTORS[G]
        else:
            minImpactFactors[i] = IMPACT_FACTORS[T]            
    
    return minImpactFactors
```

# Min Avg Two Slice

A non-empty array A consisting of N integers is given. A pair of integers (P, Q), such that 0 ≤ P < Q < N, is called a slice of array A (notice that the slice contains at least two elements). The average of a slice (P, Q) is the sum of A[P] + A[P + 1] + ... + A[Q] divided by the length of the slice. To be precise, the average equals (A[P] + A[P + 1] + ... + A[Q]) / (Q − P + 1).

For example, array A such that:

    A[0] = 4
    A[1] = 2
    A[2] = 2
    A[3] = 5
    A[4] = 1
    A[5] = 5
    A[6] = 8
contains the following example slices:

slice (1, 2), whose average is (2 + 2) / 2 = 2;
slice (3, 4), whose average is (5 + 1) / 2 = 3;
slice (1, 4), whose average is (2 + 2 + 5 + 1) / 4 = 2.5.
The goal is to find the starting position of a slice whose average is minimal.

Write a function:

class Solution { public int solution(int[] A); }

that, given a non-empty array A consisting of N integers, returns the starting position of the slice with the minimal average. If there is more than one slice with a minimal average, you should return the smallest starting position of such a slice.

For example, given array A such that:

    A[0] = 4
    A[1] = 2
    A[2] = 2
    A[3] = 5
    A[4] = 1
    A[5] = 5
    A[6] = 8
the function should return 1, as explained above.

Write an efficient algorithm for the following assumptions:

N is an integer within the range [2..100,000];
each element of array A is an integer within the range [−10,000..10,000].

## Java Solution

```java
class Solution {
    
    private int[] getPrefixSum(int[] A) {
        
        int[] prefixSum = new int[A.length];
        
        prefixSum[0] = A[0];
        
        for (int i = 1; i < A.length; ++i) {
            prefixSum[i] = prefixSum[i - 1] + A[i];
        }

        return prefixSum;
    }
    
    public double average(int[] prefixSum, int start, int end) {
    
        int subAmount = start == 0 ? 0 : prefixSum[start - 1];
        int sum = prefixSum[end] - subAmount;
        
        return sum / (double) (end - start + 1);
    }    
    
    public int solution(int[] A) {
        
        int[] prefixSum = this.getPrefixSum(A);
        
        int index = 0;
        double smallestAverage = Integer.MAX_VALUE;
    
        for (int i = 0; i < A.length - 1; ++i) {

            double twoElementAverage = this.average(prefixSum, i, i + 1);
            
            if (twoElementAverage < smallestAverage) {
                smallestAverage = twoElementAverage;
                index = i;
            }

            if (i == A.length - 2) {
                break;
            }
            
            double threeElementAverage = this.average(prefixSum, i, i + 2);

            if (threeElementAverage < smallestAverage) {
                smallestAverage = threeElementAverage;
                index = i;
            }
        }

        return index;
    }   
}
```

## Python Solution

```python
import sys

def get_prefix_sum(A):
    
    prefix_sum = [0] * len(A)
    prefix_sum[0] = A[0]
    
    for i in range(1, len(A)):
        prefix_sum[i] = prefix_sum[i - 1] + A[i]
        
    return prefix_sum
    

def average(prefix_sum, start, end):
    
    subAmount = 0 if start == 0 else prefix_sum[start - 1]
    
    return (prefix_sum[end] - subAmount) / (end - start + 1)


def solution(A):

    prefix_sum = get_prefix_sum(A)

    smallestAverage = sys.maxsize
    index = 0
    
    for i in range(0, len(A) - 1):
        
        twoElementAvg = average(prefix_sum, i, i + 1)
        
        if twoElementAvg < smallestAverage:
            smallestAverage = twoElementAvg
            index = i
            
        if i == len(A) - 2:
            break
        
        threeElementAvg = average(prefix_sum, i, i + 2)
        
        if threeElementAvg < smallestAverage:
            smallestAverage = threeElementAvg
            index = i

    return index
```

# Count Div

Write a function:

class Solution { public int solution(int A, int B, int K); }

that, given three integers A, B and K, returns the number of integers within the range [A..B] that are divisible by K, i.e.:

{ i : A ≤ i ≤ B, i mod K = 0 }

For example, for A = 6, B = 11 and K = 2, your function should return 3, because there are three numbers divisible by 2 within the range [6..11], namely 6, 8 and 10.

Write an efficient algorithm for the following assumptions:

A and B are integers within the range [0..2,000,000,000];
K is an integer within the range [1..2,000,000,000];
A ≤ B.

## Java Solution

```java
class Solution {
    public int solution(int A, int B, int K) {
        return B / K - A / K + (0 == A % K ? 1 : 0);
    }  
}
```

## Python Solution

```python
def solution(A, B, K):
    return B // K - A // K + (1 if A % K == 0 else 0)
```

