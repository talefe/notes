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
An extra example you can do is simply to start your netcat listening on port 8080 `nc -l 8080` and performing a request with your browser to your localhost in order to should your cadets a clear request as it arrives to a webserver.



[http-status]:resources/images/http-status.jpg
