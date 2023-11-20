# Lab Report 4

## Part 1

### A failure-inducing input for the buggy program, as a JUnit test and any associated code
```ruby
@Test
  public void test(){
  int[] input2={3,5,6,5};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{ 5,6,5,3}, input2);
  
  }

```

### An input that doesn’t induce a failure, as a JUnit test and any associated code 

```ruby
@Test 
	public void testReverseInPlace() {
    int[] input1 = { 3 };
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{ 3 }, input1);
	}
```

### The symptom, as the output of running the tests 

![Image](Symptom.png)

### The bug, as the before-and-after code change required to fix it 
Before:
```ruby
static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

After:
```ruby
  static void reverseInPlace(int[] arr){
  for (int i = 0; i < arr.length / 2; i++) {
        
        int temp = arr[i];
        arr[i] = arr[arr.length - i - 1];
        arr[arr.length - i - 1] = temp;
    }
}
```

Previously, the first element was being changed to the last element and the first element wasn't stored. Thus, when the for loop tries to change the last element to the first element. It is just changing it to the newly stored first element, which is the last element. This problem was there for the entirety of the second half of the array as they were just being changed to themselves. Hence, there was the bug. The new code is changing the first element to the last element and storing the previous value of the first element and then setting that to the value of the last element in the same iteration of the for loop.This pattern is being repeated for all the other elements. Thus, the values are actually being swapped and reversed as the first element is being swapped with the last element. This is the same for the second last element and the second element and so on. Additonally, the for loop only runs for half of the length of the array as two element values are being changed in each iteration.











