# ****How Web Works Exercise****

## **Part One: Solidify Terminology**

In your own terms, define the following terms:

- What is HTTP?   <span style ="color: yellow;">Hypertext Transfer Protocal. How browsers
 servers communicate.</b></span>
- What is a URL?  <span style ="color: yellow;">Uniform Resource Locator. A URL is the address 
  of a given unique resource on the Web. </b></span>
- What is DNS?  <span style ="color: yellow;">Domain Name System, translate human readable domain names 
  to machine readable IP addresses </b></span>
- What is a query string?  <span style ="color: yellow;">Part of an (URL) that assigns values to specified parameters</b></span>
- What are two HTTP verbs and how are they different? <span style ="color: yellow;">GET requests without side effects, while 
  POST requests with side effects such as changing data on the server</b></span>
- What is an HTTP request?   <span style ="color: yellow;">HTTP works as a request-response protocol between a client 
  and server. The aim of the request is to access a resource on the server from the client.</b></span>
- What is an HTTP response?   <span style ="color: yellow;">A HTTP response is made by a server to a client. The aim 
  of the response is to provide the client with the resource it requested, or inform the client that the action it 
  requested has been carried out</b></span>
- What is an HTTP header?  <span style ="color: yellow;"> HTTP headers are used to pass additional
  information between the clients and the server through the request and response header. Some of the information in a header
  is Source IP address and port number. Requested URI (data or web page)</b></span>
  Give a couple examples of request and response headers you have seen.  <span style ="color: yellow;">RESPONSE HEADERS: Content-Type: text/html,
   Location: /error.html REQUEST HEADERS:  Hostname you are asking about, Language, date.</b></span>
- What are the processes that happen when you type “http://somesite.com/some/page.html” into a browser?
  <span style ="color: yellow;">A GET URL request goes out and returns 302(Moved Temporarily). It gets redirected and more GETS requests for 
  js, css, image, and other URL's (status code 200). I then see some OPTION request to check and see which options are allowed and if 
  it's coming from an allowed  source (status code 200). I then see some POST's for setting cookies, and some json (status code 200).
   The browser sets up the page with the redirected "The domain somesite.com is for sale" page.  I then see some addition GET's 
   requesting additional information status (204 No Content)</b></span>
## ****Part Two: Practice Tools****

1. Using ***curl***, make a ***GET*** request to the *icanhazdadjoke.com* API to find all jokes involving the word “pirate” \
<span style ="color: yellow;">  
curl -H "Accept: application\/json" "https:\/\/icanhazdadjoke.com/search?term=pirate"   \
{"current_page":1,"limit":20,"next_page":1,"previous_page":1,"results": \
[\
    {"id":"2gii3LeN7Ed","joke":"Why couldn't the kid see the pirate movie? Because it was rated arrr!"}, \
    {"id":"QuscibaMClb","joke":"What does a pirate pay for his corn? A buccaneer!"}, \
    {"id":"SvzIBAQS0Dd","joke":"What did the pirate say on his 80th birthday? Aye Matey!"}, \
    {"id":"SnOf2gqjiqc","joke":"Why are pirates called pirates? Because they arrr!"}, \
    {"id":"exXSCtkOKe","joke":"Why do pirates not know the alphabet? They always get stuck at \"C\"."} \
] \
,"search_term":"pirate","status":200,"total_jokes":5,"total_pages":1} </b></span>
2. Use ***dig*** to find what the IP address is for *icanhazdadjoke.com* (see underlined below for v4 v6 IP'scl)  
<span style ="color: yellow;">$ dig icanhazdadjoke.com \
\; \<\<\>\> DiG 9.16.1-Ubuntu <<>> icanhazdadjoke.com \
\;\; global options: +cmd \
\;\; Got answer: \
\;\; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 31433 \
\;\; flags: qr rd ad; QUERY: 1, ANSWER: 2, AUTHORITY: 0, ADDITIONAL: 0 \
\;\; WARNING: recursion requested but not available \
\;\; QUESTION SECTION: \
\;icanhazdadjoke.com.            IN      A  \
\;\; ANSWER SECTION:  </b></span>  
<u> icanhazdadjoke.com.     0       IN      A       104.21.66.15</u> \
<u> icanhazdadjoke.com.     0       IN      A       172.67.198.173</u>  
<span style ="color: yellow;">\;\; Query time: 21 msec \
\;\; SERVER: 172.19.80.1#53(172.19.80.1) \
\;\; WHEN: Thu Sep 07 22:52:26 EDT 2023 \
\;\; MSG SIZE  rcvd: 86</b></span> 
3. Make a simple web page and serve it using ***python3 -m http.server***. Visit the page in a browser.\
<span style ="color: yellow;">$ python3 -m http.server \
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ... \
127.0.0.1 - - [07/Sep/2023 23:44:13] "GET / HTTP/1.1" 200 - \
127.0.0.1 - - [07/Sep/2023 23:44:31] "GET /webExercise.html HTTP/1.1" 200 - \
127.0.0.1 - - [07/Sep/2023 23:44:57] "GET /webExercise.html HTTP/1.1" 304 -</b></span>

## ***Part Three: Explore Dev Tools***

Build a very simple HTML form that uses the GET method (it can use the same page URL for the action) when the form is submitted.

Add a field or two to the form and, after submitting it, explore in Chrome Developer tools how you can view the request and response headers.
<span style ="color: yellow;"><\!DOCTYPE html\> \
\<html lang="en"\> \
\<head\> \
    \<meta charset="UTF-8"\> \
    \<meta name="viewport" content="width=device-width, initial-scale=1.0"\> \
    \<title\>Document\</title\>  \
\</head\>  \
\<body\>   \
   \<h2\>Hello America!!</h2\>  \
   \<form action= "http://localhost:8000" method= "get"\>             
    \<h2\>Tesing GET\</h2\>  \
    \<input type="text" name ="GET"\>   \
     \<br\>\<br\> \
     \<button type="submit"\> \
        Submit 
     \</button\> \
   \</form\> \ 
  \<br\>\<br\>  \
    \<form action= "http://localhost:8000" method= "post"\>             
    \<h2\>Tesing POST\</h2\>  \
    \<input type="text" name ="POST"\> \
    \<br\>\<br\> \
     \<button type="submit"\> \
        Submit 
     \</button\> \
   \</form>\
\</body\> \
\</html\> \
</b></span>

<span style ="color: yellow;">Request URL: \
http:\/\/localhost:8000\/?GET=This+is+a+get+test \
Request Method: \
GET   \
Status Code: \
200 OK   \
Remote Address:  \
127.0.0.1:8000   \
Referrer Policy:  \
strict-origin-when-cross-origin </b></span> 



Edit the page to change the form type to POST, refresh in the browser and re-submit. Do you still see the field in the query string? Explore in Chrome how you can view the request and response headers, as well as the form data.
<span style ="color: yellow;">  No.  \
Request URL: \
http:\/\/localhost:8000\/ \
Request Method: \
POST  \
Status Code:  \
501 Unsupported method ('POST')  \
Remote Address:  \
127.0.0.1:8000   \
Referrer Policy:   \
strict-origin-when-cross-origin </b></span>   


## **Part Four: Explore the URL API**

At times, it’s useful for your JavaScript to look at the URL of the browser window and change how the script works depending on parts of that (particularly the query string).

[Read about the URL API](https://developer.mozilla.org/en-US/docs/Web/API/URL)

Try some of the code examples in the Chrome Console so that you can get comfortable with the basic methods and properties for instances of the URL class.
 <span style ="color: yellow;"></b>Done.</span>

