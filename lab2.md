# Lab 2 Report

## Part 1: WebServer.java Code
---

``` 
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;

class Handler implements URLHandler {
    // The one bit of state on the server: a number that will be manipulated by
    // various requests.
    String userMessages = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) {
            String[] parameters = url.getQuery().split("&");
            String[] msgParams = parameters[0].split("=");
            String[] userParams = parameters[1].split("=");
            userMessages += userParams[1] + ": " + msgParams[1] + "\n";
            return userMessages;
        }  
        return "404 Not Found!"; 
    }
}

class ChatServer {
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

## Using the add command

#### Example 1:

![Image](lab2-img/msg2.png)

Before getting to the screenshot, the first method called is the `main` method, which starts the server on the specified port when we run `java WebServer <port>` in the terminal. 

In this screenshot, the `handleRequest` method within the `Handler` class is called. It takes a `URI` argument named `url`, which in this case is literally our url: `http://localhost:4092/add-message?s=goodbye&user=John`. The only field I created in the `Handler` class is the String `userMessages`. It starts off blank, but once we perform this request, we concatenate specific request data to the `userMessages` variable. Namely, we add the user (`john`), a colon (`: `), the message (`goodbye`), and finally a new line `\n`, so that when we add the next person's message, it is on a different line despite being part of the same String variable. Thus `userMessages` is equal to the string `"John: goodbye \n"`.

---
#### Example 2:

![Image](lab2-img/msg1.png)

Like in the last example, the `handleRequest` method is called. It takes our `URI` argument with the specific url we used, that being `http://localhost:4092/add-message?s=Hello&user=NiroopK`. At this point, our String field variable (`userMessages`) is currently equal to `"John: goodbye \n"` due to our earlier request. With this second add-message request, we concatenate the "Hello" message by user "NiroopK" to the `userMessages` field variable. Thus, the value of this String field becomes `"John: goodbye \n NiroopK: Hello \n"`, which will be displayed much more neatly on the site thanks to the "\n" newlines (the output can be seen in the screenshot above).
