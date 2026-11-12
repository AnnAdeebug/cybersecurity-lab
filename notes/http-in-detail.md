# Room: HTTP in details

## Task 1: What's HTTPS?
* HTTP: HyperText Transfer Protocol - set of rules used for communicating with web servers for transmitting webpage data
* HTTPS: HyperText Transfer Protocol Secure - secure version of HTTP, encrypted

## Task 2: Request & Response
* URL: Uniform Resource Locator - predominantly an instruction on how to access a resource on the internet
* e.g URL & features:

| http:// | user:password | @tryhackme.com | :80 | /view-room? | id=1 | #task3 |
|---------|---------------|----------------|-----|-------------|------|--------|
|scheme | user | host/domain | port | path | query string | fragment |

* Making request:

| Example Request | explanation | 
|-----------------|-------------|
| GET / HTTP/1.1   | get method / using http / version 1.1 |
|                 |             |
| Host: tryhackme.com | tell server we want website tryhackme |
| User-Agent: Mozilla/5.0 Firefox/87.0 | tell server we use firefox version 87 browser |
| Referer: https://tryhackme.com/ | tells the server which page I came from |

A request ends with a blank line to show it is finished. 


## Task 3: HTTP Methods
* GET : get data
* POST : create new data
* PUT : update data
* DELETE : remove data

## Task 4: HTTP Status codes

| Code | Status |
|------|--------|
| 100-199 | information response |
| 200-299 | success |
| 300-399 | redirection |
| 400-499 | client errors |
| 500-599 | server errors |

common code:
| code | status |
|------|--------|
| 200-OK | Request successfully work, data given|
| 201-Created | New thing is made, usually after a POST |
| 301-Moved Permanently | Page moved to new URL|
| 302-Found | temporary redirect, old URL still exists|
| 400-Bad Request | server could not understand the request |
| 401-Unauthorized| login invalid/missing |
| 403-Forbidden | not allowed |
| 404-Not Found | path does not exist |
| 405-Method Not Allowed | wrong method |
| 500-Internal Server Error | something wrong on the server side |
| 503-Service Unavailable | server overloaded/down for maintenance |

## Task 5: Headers
* Common request headers:
	- Host: tells the server which website I want, since one server can host many sites, otherwise receive default website for the server
	- User-Agent: tells the server which browser/device i am using
	- Content-Length: tells the web server how much data to expect in the web request, so server know no missing data 
	- Accept-Encoding: tells the web server types of compression methods the browser supports
	- Cookie: Data sent to the server to help remember your information

* Common response headers:
	- Set-Cookie: server tells my browser to save a cookie
	- Cache-Control: How long to store the content of the response in the browser's cache before it requests it again.
	- Content-Type: tells the browser what type of data is being returned
	- Content-Encoding: What method has been used to compress the data 

## Task 6: Cookie
* cookie: small piece of data that is stored in my browser. most commonly used for website authentication. the cookie value is like token; unique secret code 

* Why this matters
- HTTP sends data in plain text; HTTPS encrypts it, so passwords
  sent over HTTP can be read by someone on the network.
- Cookies keep me logged in. If someone steals a session cookie,
  they could act as me.
- Many 401/403 responses in a row from one IP in logs could mean
  someone is guessing logins or probing for pages.
- As a tester: in Postman I check the status code, e.g. 404 for a
  missing resource, 400 for bad input, 401 for no token.

## Task 7: Making Request
Lab test in the server - using emulator to make demo HTTP requests

1. method: GET request to /room page 
- result: 200 OK
- Welcome to the Room page

2. method: GET request to /blog page set id parameter = 1
- result: 200 OK
- Viewing Blog article 1 

3. method: DELETE request to /user/1 page
- result: 200 OK
- The user has been deleted

4.	method: PUT request to /user/2 page set username parameter admin
- result: 200 OK
- Username changed to admin

5.	method: POST request to /login page set username thm and a sample password 
- result: 200 OK
- You logged in! Welcome Back

additional, not in instruction requests:
6.	method: GET request to /home page 
- result: 404 Not Found
- cannot find page

7.	method: GET request to /blog page set id parameter = 99
- result: 404 Not Found
- invalid blog id 

8.	method: DELETE request to /user/2 page
- result: 404 Not Found
- cannot find page

9.	method: PUT request to /user/2 page without set username parameter admin
- result: 400 Bad Request
- Missing parameter

10.	method: POST request to /login page without username and password
- result: 400 Bad Request
- Missing post parameter

Learned: the same endpoint can return 200, 404 or 400 depending on the input. This is what I have tested in API testing
