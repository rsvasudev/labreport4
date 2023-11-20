# Lab Report 4

## Part 1

### A failure-inducing input for the buggy program, as a JUnit test and any associated code
```ruby
@Test
public void test(){
  int[] input2={3,5,6,5};
  ArrayExamples.reverseInPlace(input2);
  assertArrayEquals(new int[]{5,6,5,3}, input2);
  
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

Previously, the first element was being changed to the last element and the first element wasn't stored. Thus, when the for loop tries to change the last element to the first element. It is just changing it to the newly stored first element, which is the last element. This problem was there for the entirety of the second half of the array as they were just being changed to themselves. Hence, there was the bug. 

For example, using the example I had with the array {3,5,6,5}.
In the first iteration of the for loop, the first element is given the value of the last element. Thus, the array becomes {5,5,6,5}
Similarly, in the second iteration, the array becomes {5,6,6,5}. The second element is given the value of the the third element
In the third iteration, the array becomes {5,6,6,5}. The third element is given the value fo the new second element(6). Thus, the array stays the same. At this point, the array should become {5,6,5,5} but the old second value isnt stored so the thrid element is instead assigned the new value fo the second element.
Lastly, in the next iteration, the array becomes {5,6,6,5} as the last element is given the new value of the first element instead of becoming {5,6,5,3}. Thus, you can see the bug that appears in reversing the second half of the array as it is just reassigned the same value. 

The new code is changing the first element to the last element and storing the previous value of the first element and then setting that to the value of the last element in the same iteration of the for loop.This pattern is being repeated for all the other elements. Thus, the values are actually being swapped and reversed as the first element is being swapped with the last element. This is the same for the second last element and the second element and so on. Additonally, the for loop only runs for half of the length of the array as two element values are being changed in each iteration.

Again, using the same array as an example: {3,5,6,5}.
In the first iteration, the first and last elements are swapped. Thus, the array becomes {5,5,6,3}
In the second and last iteration, the second and third elements are swapped. Thus, the array becomes {5,6,5,3}, which is the correct solution. 
Therefore, the bug is fixed.

### Proof of symptom being fixed

![Image](Fixed.png)

## Part 2












