## CSE15L Lab Report 2
---
# Part 1:
__Chatserver code:__
```
# code block
import java.io.IOException;
import java.net.URI;

class ChatHandler implements URLHandler {

    private StringBuilder chatHistory = new StringBuilder();

    public String handleRequest (URI url) {
        if (url.getPath().equals("/add-message")) {
            String query = url.getQuery();
            String s = null;
            String user = null;

            if (query != null) {
                for (String parameter : query.split("&")) {
                    String[] param = parameter.split("=");
                if (param.length == 2) {
                    if (param[0].equals("s")) {
                        s = param[1];
                    } else if (param[0].equals("user")) {
                        user = param[1];
                    }
                 }
             }
         }
            if (s != null && user != null) {
                chatHistory.append(String.format("%s: %s\n", user, s));
                return chatHistory.toString();
            }
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

        Server.start(port, new ChatHandler());
    }
}
```

__Output 1:__
![Image](example1.png)
-Which methods in your code are called?
The method handle in ServerHttpHandler gets called as a request is being made within the web server (/add-message?s=CSE15L&user=paola).
Afterwards, the method handleRequest in ChatHandle is called to handle the paths.
-What are the relevant arguments to those methods, and the values of any relevant fields of the class?
The argument relevant to ServerHttpHandler.handle is exchange as the HttpExchange gets the request URI and gives it to the handleRequest method in
 ChatHandler. Thus, ChatHandler.handleRequest has the args url, which is the request URI (/add-message).
-How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
A relevant field to the ChatHandler class is chatHistory, which stores the chat messages as a StringBuilder object. The chatHistory field gets modified
by handleRequest method when a new message is appended. 

__Output 2:__
![Image](example2.png)
-Which methods in your code are called?
In this example, the method handleRequest from ChatHandler is being called to check the path and if it fits the criteria.
-What are the relevant arguments to those methods, and the values of any relevant fields of the class?
There are no relevant arguments to those methods as "404 Not Found" is the default response to an incorrect request path and not stored as a chat message.
-How do the values of any relevant fields of the class change from this specific request? If no values got changed, explain why.
There are no field changes because this is just the expected output that appears with there is no request.

---
# Part 2:
-The absolute path to the private key for your SSH key for logging into ieng6 (on your computer, an EdStem workspace, or on the home directory of the lab computer)
![Image](privatekey.png)
-The absolute path to the public key for your SSH key for logging into ieng6 (this is the one you copied to your account on ieng6, so it should be a path on ieng6's file system)
![Image](publickey.png)
___
# Part 3:
As I am new to Git and Github, I have learned many new techniques within that realm. I am now more familiar with setting up SSH keys on my own personal account, as I didn't know they existed before.
Furthermore, I have learned how to access web servers and new terminology within code, such as commands like mkdir (make directory) and scp command(copies files and directories). This new knowledge
will be extremely helpful in the future when navigating code. Although I still have a lot more to learn, I feel more comfortable when using web servers and git.