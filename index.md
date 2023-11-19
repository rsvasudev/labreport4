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





