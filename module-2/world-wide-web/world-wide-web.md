####Http status
Whenever a server answers a client, part of the response is an http status code in order to inform the client of how he's supposed to interpret the response. Here's an easy way to remember those:

![HTTP-status][http-status]

####**curl** and **wget**
Both **curl** and **wget** are command line tools able to download content through FTP, HTTP and HTTPS protocols.
They can also send POST requests, support HTTP cookies, and can work without user interaction, like being used from within scripts. Always remember there are `man` pages if you need to check for specific usage or meaning of the flags in the examples.

######**curl** examples

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

####**wget** examples
With **wget** you can rercursively download entire sites to your machine, for example
`wget -r t1 www.gnu.org`

You can recursively download (`-r`), span hosts (`-H`), convert links to local versions (`--convert links`), and set the level of recursion (`-level=<NUMBER>`, use `0` for infinite);
Since some sites don't allow you to download recursively and will check what browser you are using in an attempt to block the bot, we can declare a user agent such as Mozilla to get around this (`-user-agent=<AGENT>`);

`wget -r -H --convert-links --level=NUMBER --user-agent=AGENT URL`


[http-status]:resources/images/http-status.jpg
