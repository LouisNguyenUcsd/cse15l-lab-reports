Lab report 3
Part 1: Bugs
Provide:

// Changes the input array to be in reversed order
```
static void reverseInPlace(int[] arr) {
  for (int i = 0; i < arr.length; i++) {
    arr[i] = arr[arr.length - i - 1];
  }
}
```

Failure Inducing Input                      

```
public void testReverseInPlace(){
  int[] input = {5, 4, 0, 3, 5};
    ArrayExamples.reverseInPlace(input);
    assertArrayEquals(new int[]{5, 3, 0, 4, 5 input);
  }
 ```  
                      







                      
                      
          
                      
                    

