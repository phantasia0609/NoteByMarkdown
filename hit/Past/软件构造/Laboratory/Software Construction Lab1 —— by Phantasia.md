### ArrayIndexOutOfBoundException

> **_ArrayIndexOutOfBoundsException_ occurs when we access an array, or a _Collection_, that is backed by an array with an invalid index.** This means that the index is either less than zero or greater than or equal to the size of the array.
- 也就是说，使用 index 索引数组的时候可能出现了*负数*或者是*大于数组长度的数*

#### 可能出错的情况
##### 越界访问数组
> **Accessing the array elements out of these bounds would throw an _ArrayIndexOutOfBoundsException_:**
``` java
int[] numbers = new int[] {1, 2, 3, 4, 5};
int lastNumber = numbers[5];
```
> Here, the size of the array is 5, which means the index will range from 0 to 4.
  In this case, accessing the 5th index results in an _ArrayIndexOutOfBoundsException_:
``` java
Here, the size of the array is 5, which means the index will range from 0 to 4.

In this case, accessing the 5th index results in an _ArrayIndexOutOfBoundsException_:
```

##### 访问由 Arrays.asList() 返回的 List
> **If we try to access the elements of the _List_ returned by _Arrays.asList()_ beyond this range, we would get an _ArrayIndexOutOfBoundsException_:**
``` java
List<Integer> numbersList = Arrays.asList(1, 2, 3, 4, 5);
int lastNumber = numbersList.get(5);
```
> Here again, we are trying to get the last element of the _List_. The position of the last element is 5, but its index is 4 (size – 1). Hence, we get _ArrayIndexOutOfBoundsException_ as below:
```  java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
    at java.base/java.util.Arrays$ArrayList.get(Arrays.java:4351)
    at  ...
```

##### 循环遍历数组
>**Sometimes, while iterating over an array in a for loop, we might put a wrong termination expression.**

>Instead of terminating the index at one less than the length of the array, we might end up iterating until its length:

```java
int sum = 0;
for (int i = 0; i <= numbers.length; i++) {
    sum += numbers[i];
}
```

> In the above termination expression, the loop variable _i_ is being compared as less than or equal to the length of our existing array _numbers._ So, in the last iteration, the value of _i_ will become 5.

> Since index 5 is beyond the range of _numbers,_ it will again lead to _ArrayIndexOutOfBoundsException_:

```java
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: Index 5 out of bounds for length 5
    at com.baeldung.concatenate.IndexOutOfBoundExceptionExamples.main(IndexOutOfBoundExceptionExamples.java:22)
```
#### Avoid  This Exception
- Remembering the index
- Correctly Using the Operators in Loops
- Using Enhanced for Loops (using iterator)


### NegativeArraySizeException
#### 什么导致了NegativeArraySizeException in Java

The `NegativeArraySizeException` occurs when an attempt is made to assign a negative size to an array. Here's an example:

``` java
public class NegativeArraySizeExceptionExample {
    public static void main(String[] args) {
        int[] array = new int[-5];
        System.out.println("Array length: " + array.length);
    }
}
```

Running the above code throws the following exception:

``` java
Exception in thread "main" java.lang.NegativeArraySizeException: -5
    at NegativeArraySizeExceptionExample.main(NegativeArraySizeExceptionExample.java:3)
```

#### 怎么解决 NegativeArraySizeException in Java

The `NegativeArraySizeException` can be handled in code using the following steps:

- Surround the piece of code that can throw an `NegativeArraySizeException` in a `try-catch` block.
- Catch the `NegativeArraySizeException` in the `catch` clause.
- Take further action as necessary for handling the exception and making sure the program execution does not stop.

Here's an example of how to handle it in code:

``` java
public class NegativeArraySizeExceptionExample {
    public static void main(String[] args) {
        try {
            int[] array = new int[-5];
        } catch (NegativeArraySizeException nase) {
            nase.printStackTrace();
            //handle the exception
        }
        System.out.println("Continuing execution...");
    }
}
```

In the above example, the lines that throw the `NegativeArraySizeException` are placed within a `try-catch` block. The `NegativeArraySizeException` is caught in the `catch` clause and its stack trace is printed to the console. Any code that comes after the `try-catch` block continues its execution normally.

Running the above code produces the following output:

``` java
java.lang.NegativeArraySizeException: -5
    at NegativeArraySizeExceptionExample.main(NegativeArraySizeExceptionExample.java:4)
Continuing execution...
```

#### 怎么避免 NegativeArraySizeException in Java

Since the `NegativeArraySizeException` occurs when an array is created with a negative size, assigning a positive size to the array can help avoid the exception. Applying this to the earlier example helps fix the issue:

``` java
public class NegativeArraySizeExceptionExample {
    public static void main(String[] args) {
        int[] array = new int[5];
        System.out.println("Array length: " + array.length);
    }
}
```

The array is initialized with a size of 5, which is a positive number. Running the above code produces the correct output as expected:

```
Array length: 5
```

---
reference：
- [JAVA ArrayIndexOutOfBoundsException][https://www.baeldung.com/java-arrayindexoutofboundsexception]
- [NegativeArraySizeException][https://rollbar.com/blog/java-negativearraysizeexception/]