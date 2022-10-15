# Week 3 Lab Report - Search Engine and Debugging

## **Part 1**
*Simple Search Engine*

The code for my Search Engine can be found below

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

* The image above shows an example of adding the string "apple" to the list of strings that the web server tracks using the variable strsList.

* In this case, the handleRequest(URI url) method is being called, which uses the url parameter to understand what functions the web server must perform.

* This is done using the getPath() method followed by the getQuery() method if the url path indicates that one of the allowed queries will follow (add or search).

* For my Search Engine, the add function adds a string to strsList, and displays the string that is being added on the screen.

 ***Add Again***

![Image](/images/AddBanana.png)

* Similar to the first image, the image above shows the string "banana" being added to strsList.

* The handleRequest() with the parameter url, getPath(), and getQuery() methods are also once again used.

* Before "banana" was added to strsList, the string "pineapple" was also added, both of which will be used in the next section to demonstrate the search query.

***Search Query***

![Image](/images/SearchApple.png)

* The above image shows an example of the search query being used, with the string "apple" being passed into the query.

* Similar to add, the handleRequest() with the parameter url, getPath(), and getQuery() methods are used, with getQuery() being used to recognize what string to search for and getPath() being used to check for any queries.

* For my search engine, the search query iterates through the ArrayList strsList that contains all of the strings that have been added.

* As it iterates, if a string in strsList contains the string passed into the query, it is concatenated onto a string called str with a space character.

* Once the loop finishes, str is returned to indicate what strings that have been added match the search query.

## **Part 2**
*Debugging*

