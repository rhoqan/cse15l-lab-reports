# Week 3 Lab Report - Search Engine and Debugging

## **Part 1**
*Simple Search Engine*

The code for my Search Engine can be found below:

```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    int num = 0;
    List<String> strsList = new ArrayList<>();
    String str = "";


    public String handleRequest(URI url) {
        if (url.getPath().equals("/")) {
            return String.format("Number: %d", num);
        } else if (url.getPath().equals("/increment")) {
            num += 1;
            return String.format("Number incremented!");
        } else {
            System.out.println("Path: " + url.getPath());
            if (url.getPath().contains("/add")) {
                String[] parameters = url.getQuery().split("=");
                if (parameters[0].equals("s")) {
                    strsList.add(parameters[1]);
                }
                return parameters[1];
            }
            if (url.getPath().contains("/search")) {
                String[] parameters = url.getQuery().split("=");
                str = "";
                for (String s: strsList) {
                    if (s.contains(parameters[1])) {
                        str += s + " ";
                    }
                }
                return str;
            }
            return "404 Not Found!";
        }
    }
}
class SearchEngine {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }    
}
```

***Add Function***

![Image](/images/SearchEngineAdd.png)

* The image above shows an example of adding the String `"apple"` to the list of Strings that the web server tracks using an ArrayList called `strsList`.

* In this case, the `handleRequest(URI url)` method is being called, which uses the url parameter to understand what functions the web server must perform.

* This is done using the `getPath()` method followed by the `getQuery()` method if the url path indicates that one of the allowed queries will follow (add or search).

* For my Search Engine, the add function adds a String to `strsList`, and displays the String that is being added on the screen.

 ***Add Again***

![Image](/images/AddBanana.png)

* Similar to the first image, the image above shows the String `"banana"` being added to strsList.

* The `handleRequest()` with the parameter url, `getPath()`, and `getQuery()` methods are also once again used.

* Before `"banana"` was added to `strsList`, the String `"pineapple"` was also added, both of which will be used in the next section to demonstrate the search query.

***Search Query***

![Image](/images/SearchApple.png)

* The above image shows an example of the search query being used, with the String `"apple"` being passed into the query.

* Similar to add, the `handleRequest()` with the parameter url, `getPath()`, and `getQuery()` methods are used, with `getQuery()` being used to recognize what String to search for and `getPath()` being used to check for any queries.

* For my search engine, the search query iterates through the ArrayList `strsList` that contains all of the Strings that have been added.

* As it iterates, if a String in `strsList` contains the String passed into the query, as checked through the String `contains()` method, it is concatenated onto a String called `str` with a space character.

* Once the loop finishes, `str` is returned to indicate what Strings that have been added match the search query.

## **Part 2**
*Debugging*

**Bug 1**

The code below shows the failure-inducing input:

```
  @Test
  public void testReversedInPlaceWithMore() {
    int[] input1 = {1, 9, 24, 36};
    ArrayExamples.reverseInPlace(input1);
    assertArrayEquals(new int[]{36, 24, 9, 1}, input1);
  }
```

The image below shows the symptom:

![Image](/images/Bug1Symptom.png)

* The `reverseInPlace()` method changes the original array into one with the elements `{36, 24, 24, 36}` instead of `{36, 24, 9, 1}` as expected.

The code below is the original code:

```
 static void reverseInPlace(int[] arr) {
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = arr[arr.length - i - 1];
    }
  }
```

* The particular bug in this case is that `reverseInPlace()` does not use a temporary variable to store the values of the original array.

* This causes the symptom because `reverseInPlace()` as the elements in the latter half of the array will be updated to the wrong numbers as the elements they are supposed to be updated to are no longer accessible.

* Using a temporary variable to store the elements of the original array ensures that they remain accessible.

The code below fixes the bug:

```
 static void reverseInPlace(int[] arr) {
    int[] oldArray = new int[arr.length];
    for(int i = 0; i < arr.length; i += 1) {
      oldArray[i] = arr[i];
    }
    for(int i = 0; i < arr.length; i += 1) {
      arr[i] = oldArray[arr.length - i - 1];
    }
  }
```

**Bug 2**

The code below shows the failure-inducing input:

```
   @Test
	public void testAppend() {
		LinkedList l_list1 = new LinkedList();
		l_list1.append(2);
		l_list1.append(3);
		l_list1.append(5);
		l_list1.append(7);
		String expectedString = "2 3 5 7 ";
        assertEquals(expectedString, l_list1.toString());
	}
```

The image below shows the symptom:

![Image](/images/Bug2Symptom.png)

* The `append()` method results in an infinite loop that eventually causes a `java.lang.OutOfMemoryError`

The code below is the original code:

```
    public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
            n.next = new Node(value, null);
        }
    }
```

* The particular bug in this case is in the `while` loop at the bottom.

* If the number of elements in the existing LinkedList is greater than 1, the `while` loop at the bottom is executed.

* The problem is caused by the loop creating a new `Node` object each time the loop runs and setting `n.next` equal to it.

* Therefore, `n.next` will never be null, causing the infinite loop.

* The fix needed would be to move the line `n.next = new Node(value, null);` to outside of the while loop so that only one new `Node` object is added once the end of the list is reached.

The code below fixes the bug:

```
public void append(int value) {
        if(this.root == null) {
            this.root = new Node(value, null);
            return;
        }
        // If it's just one element, add if after that one
        Node n = this.root;
        if(n.next == null) {
            n.next = new Node(value, null);
            return;
        }
        // Otherwise, loop until the end and add at the end with a null
        while(n.next != null) {
            n = n.next;
        }
        n.next = new Node(value, null);
    }
```
