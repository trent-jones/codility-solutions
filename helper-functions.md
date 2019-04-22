# Java

## Print Array

```java
    private void printArray(int[] A) {

        System.out.print("[");

        for (int i = 0; i < A.length; ++i) {
            
            if (i < A.length - 1) {
                System.out.print(A[i] + ", ");
            } else {
                System.out.println(A[i] + "]");
            }
        }
    }
```



# Go

## Absolute Value of int

```go
func abs(x int) int {
    
    if x < 0 {
        return -x
    }
    
    return x
}
```

