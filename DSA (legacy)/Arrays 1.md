Array is a fundamental data structure that
- Stores a fixed number of elements
- All elements must be of the same datatype
- All the elements has a unique index, starting from 0
- The Size of the array is predefined and cannot be modified.
- The Array elements are contagious in memory, meaning each element is located next to each other
### Why do we need an Array?
What if we need 300 variables? Array is your savior.
## Creating an array
```java
// one dimensional
class Main{
	public static void main(String args[]){
		int[] intArray;           // declaration
		intArray = new int[3]     // instatiation
		intArray[0] = 2

		String sArray[] = {"asdf","df",'f'};
	}
}

// two dimensional
class Main{
	public static void main(String args[]){
		int[][] intArray;
		intArray = new int[3][3]

		
	}
}
```
## Printing out the array 
```java
import java.util.Arrays;

System.out.println(Arrays.toString(intArray))

System.out.println(intArray) // just gives -> 0xasdf
```
## Implementation of array as classes
```java
class SingleDimensionalArray{
    int arr[] = null;

    public SingleDimensionalArray(int size){
        arr = new int[size];
        for(int i = 0; i < size; i++){
            arr[i] = Integer.MIN_VALUE;
        }
    }

    public void insert(int location, int valueToBeInserted){
        try{
            if(arr[location] == Integer.MIN_VALUE){
                arr[location] = valueToBeInserted;
                System.out.println("Element inserted at location " + location);
            }
            else{
                System.out.println("Element already exists at location " + location);
            }
        } catch(ArrayIndexOutOfBoundsException e){
            System.out.println("Invalid location");
        }
    }

    public void delete(int value){
        for(int i = 0; i < arr.length; i++){
            if(arr[i] == value){
                arr[i] = Integer.MIN_VALUE;
                System.out.println("Element deleted at location " + i);
                break;
            }
        }
    }

    public void search(int value){
        for(int i = 0; i < arr.length; i++){
            if(arr[i] == value){
                System.out.println("Element found at location " + i);
                break;
            }
        }
    }
    public String toString(){
        return "The Array is: " + java.util.Arrays.toString(arr);
    }
}

public class Main{
    public static void main(String[] args){
        SingleDimensionalArray arr = new SingleDimensionalArray(10);
        arr.insert(0, 10);
        arr.insert(1, 20);
        arr.insert(2, 30);
        System.out.println(arr);

        arr.insert(3, 40);
        arr.search(30);
        arr.delete(30);
        System.out.println(arr);
    }
}
```
## Time and space complexity of 1D array

| Operation               | Time complexity | Space complexity |
| ----------------------- | --------------- | ---------------- |
| Creating an empty array | O(1)            | O(n)             |
| Inserting a value       | O(1)            | O(1)             |
| Traversing a value      | O(n)            | O(1)             |
| Accessing a given value | O(1)            | O(1)             |
| Searching a value       | O(n)            | O(1)             |
| Deleting a given value  | O(1)            | O(1)             |
## To slice an array
```java
import java.util.Arrays;
class Main{
    public static int[] middle(int[] array){
        return Arrays.copyOfRange(array, 1, array.length-1);
    }
    public static void main(String[] args){
        int array[] = {1,2,3,4};
        middle(array);
    }
}
```
***
## Find the Max Product from an Array
```python
public class Exercise {  
    public String maxProduct(int[] intArray) {  
        int min_one = Integer.MAX_VALUE;  
        int min_two = Integer.MAX_VALUE;  
        int max_one = Integer.MIN_VALUE;  
        int max_two = Integer.MIN_VALUE;  
  
        for(int elem: intArray){  
            // for two smallest numbers in the array  
            if(elem < min_one){  
                min_two = min_one;  
                min_one = elem;  
            } else if(elem < min_two){  
                min_two = elem;  
            }  
  
            // for two largest numbers in the array  
            if(elem > max_one){  
                max_two = max_one;  
                max_one = elem;  
            }else if(elem > max_two){  
                max_two = elem;  
            }  
        }  
  
        if(min_one * min_two > max_one * max_two){  
            return min_two + "," + min_one;  
        }  
        return max_two + "," + max_one;  
    }  
    public static void main(String[] args) {  
        Exercise exercise = new Exercise();  
        System.out.println(exercise.maxProduct(new int[]{-80,90,30,-60,50}));  
    }  
}
```

