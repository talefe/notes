#### Http status
Whenever a server answers a client, part of the response is an http status code in order to inform the client of how he's supposed to interpret the response. Here's an easy way to remember those:

![HTTP-status][http-status]

#### **curl** and **wget**
Both **curl** and **wget** are command line tools able to download content through FTP, HTTP and HTTPS protocols.
They can also send POST requests, support HTTP cookies, and can work without user interaction, like being used from within scripts. Always remember there are `man` pages if you need to check for specific usage or meaning of the flags in the examples.

###### **curl** examples

1. This is part of a CLI application but you can just perform a get request to its front-end. Simply replace <LOCATION> with your city, airport code or IP.
`curl http://wttr.in/<LOCATION>`
`curl wttr.in/Moon`

2. You can also expand a shortened URL in case you don't trust it for some reason
`curl -sIL http://buff.ly/1lTcZSM | grep ^Location;`

3. Another fun, although not very productive thing you can do is download ASCII animations and art.
(you might need to install the `pv` binary)
`curl -s http://artscene.textfiles\.com/asciiart/another_dragon | pv -L9600 -q`
`curl -s http://artscene.textfiles\.com/vt100/wineglas.vt | pv -L9600 -q`
`curl -s http://artscene.textfiles\.com/vt100/sship.vt | pv -L9600 -q`

4. You can get information about your public IP
`curl ipinfo.io`
Or from an external IP
`curl ipinfo.io/207.46.13.41`

#### **wget** examples
With **wget** you can rercursively download entire sites to your machine, for example
`wget -r t1 www.gnu.org`

You can recursively download (`-r`), span hosts (`-H`), convert links to local versions (`--convert links`), and set the level of recursion (`-level=<NUMBER>`, use `0` for infinite);
Since some sites don't allow you to download recursively and will check what browser you are using in an attempt to block the bot, we can declare a user agent such as Mozilla to get around this (`-user-agent=<AGENT>`);

`wget -r -H --convert-links --level=NUMBER --user-agent=AGENT URL`

**You can then use npm's http-server to locally host the site you've downloaded properly**  
(in case you don't have it, you can run `npm install http-server -g` and run it using `http-server`or `hs`)

#### **java.net.URL** examples
(the exercise "source-viewer" proposed in the slides is just the same as we see here when opening a stream and reading from it)

```java
public class JavaNetURLExample {
    public static void main(String[] args) {
        try {
            // Generate absolute URL
            // Base URL = www.gnu.org
            URL url1 = new URL("http://www.gnu.org");
            System.out.println("URL1: " + url1.toString());

            // Generate URL for pages with a common base
            URL url2 = new URL(url1, "licenses/gpl.txt");
            System.out.println("URL2: " + url2.toString());

            // Generate URLs from different pieces of data
            URL url3 = new URL("http", "www.gnu.org", "/licenses/gpl.txt");
            System.out.println("URL3: " + url3.toString());

            URL url4 = new URL("http", "www.gnu.org", 80, "/licenses/gpl.txt");
            System.out.println("URL4: " + url4.toString() + "\n");

            // Open URL stream as an input stream and print contents to command line
            try (BufferedReader in = new BufferedReader(new InputStreamReader(url4.openStream()))) {
                String inputLine;

                // Read the "gpl.txt" text file from its URL representation
                System.out.println("/***** File content (URL4) *****/n");
                while((inputLine = in.readLine()) != null) {
                    System.out.println(inputLine);
                }
            } catch (IOException ioe) {
                ioe.printStackTrace(System.err);
            }
        } catch (MalformedURLException mue) {
            mue.printStackTrace(System.err);
        }
    }
}
```


``` java
public class JavaNetURLMoreMethodsExample {
    public static void main(String[] args) {
        try {
            // Creates a URL object from the String representation.
            URL url = new URL("http://www.gnu.org/licenses/gpl.txt");

            // Gets the authority part of this URL.
            System.out.println("URL Authority: " + url.getAuthority());

            // Gets the default port number of the protocol associated with this URL.
            System.out.println("URL Default Port: " + url.getDefaultPort());

            // Gets the file name of this URL.
            System.out.println("URL File Name: " + url.getFile());

            // Gets the host name of this URL, if applicable.
            System.out.println("URL Host Name: " + url.getHost());

            // Gets the path part of this URL.
            System.out.println("URL Path: " + url.getPath());

            // Gets the protocol name of this URL.
            System.out.println("URL Protocol Name: " + url.getProtocol());
        } catch (IOException ioe) {
            ioe.printStackTrace(System.err);
        }
    }
}

```

#### **Chrome Dev-tools** guidance
The point is to start hinting cadets to how they might make use of the browser's development tools for their purposes.

To begin with you can simply open your brower of choice's tools (keep in mind cadet's machines have Google Chrome installed) and reloading the page you are on, navigate to the network tab and show them both the requests and the responses generated by that reloading, or by navigating to any given page.  
Maybe preferably choose a simple page in order to just not have too much going on at the same time in order to not intimidate the cadets.  
Checking the network traffic for [java.net.URL](https://docs.oracle.com/javase/7/docs/api/java/net/URL.html) for example should get you something relatively simple for instance.

##### Extra example
An extra example you can do is simply to start your netcat listening on port 8080 `nc -lp 8080`(the -p flag is for port, some versions of netcat require it to be declared explicitly) and performing a request with your browser to your localhost in order to should your cadets a clear request as it arrives to a webserver.

### Web-server exercise
The objective is to have the cadets implement their very first web-server.  
They will have to deal with receiving HTTP requests and answering them by using Java's TCP sockets, and they will need to grasp the understanding of how the communication with a browser occurrs (request->response).

What's intended from the cadets:

* build a server that is able to handle one request at a time
* it's a server so it shouldn't close after handling the first request
* should send a 404 response in case an unexisting resource was asked for with possibly a default html
* remember them that we will be using Java's ServerSocket and Socket classes

We can then show our web-server running and the following examples:  
(remember to open the browser's dev tools)

* access the root
* access a resource like `localhost:8080/logo.png`
* show what happens when you attemp a request to a resource that does not exist `localhost:8080/verysillyresource.html`
* remember the cadets that their responses need to start with the appropriate header and provide them with the necessary headers:

```
HTTP/1.0 200 Document Follows\r\n
Content-Type: text/html; charset=UTF-8\r\n
Content-Length: <file_byte_size> \r\n
\r\n

HTTP/1.0 200 Document Follows\r\n
Content-Type: image/<image_file_extension> \r\n"
Content-Length: <file_byte_size> \r\n
\r\n

HTTP/1.0 404 Not Found
Content-Type: text/html; charset=UTF-8\r\n
Content-Length: <file_byte_size> \r\n
\r\n
```
The new lines at the end are needed for the browser to correctly understand the response.

* If the cadets want to attempt to send more advanced files than html, like images and the such, advise them to use the DataOutputStream class as it has several handy methods such as `writeBytes(String)` and `write(File, beginning, size)`


[http-status]:resources/images/http-status.jpg
