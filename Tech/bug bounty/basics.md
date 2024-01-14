## internet 
basically it's just a globally connected devices over tcp/ip.
## tcp/ip
It's the networking protocol that the internet uses.
## http
a service used by tcp/ip to interact and display the websites.

## request
a structured piece of text sent to a http server.
## response
the reply to the received request, that the web-browser uses to display elements accordingly.

# tcp/ip handshake
- syn
- syn-ack
- ack

## dns
- basically a huge phonebook of domain-names and it's ip-address
dns provides the bridge between a domain name and ip address
### dns querying process
*when a user needs to access www.example.com*

- First, the request is sent to the ***recursive resolver*** owned by your ***ISP***
		but we need to get the ***authoritative name server***, the dude server that owns the domain.
- The search begins at the ***root name server***.
		this root name server will know all the cool kids like .com, .net, .org and stuffs (ALL THE TOP LEVEL DOMAINS **TLDs**)
- we are then redirected to the .com TLD name server and search for www.example.com
- then we can find the authoritative name server (eg. dns1.cheapbobafethosting.com)
- finally www.example.com is owned by this authoritative name server at dns1.cheapbobafethosting.com bleh bleh)

# after dns
now that the computer knows the domain's ip address and where to connect, it starts to make first contact.

- fires of port 80, for http connections
- port 443 used for https conenctions

--- 
# proxies
a tool used to capture the http requests. To modify and resend them.
==burp is a proxy==
## Http request/response
- http uses a request/response life-cycle or structure.
	- you send in a request and the server sends out a response
	- A response cannot exist without a request
- Has a envelope structure,
	- header
	- body
- headers starts with the method that's being used,
	- common - POST, GET, OPTIONS
	- APIs - PUT, DELETE
	- debug - HEAD, CONNECT, TRACE, PATCH

## status codes
- 2xx - success
	- 200 - success!
	- 204 - no content
 - 3xx - redirection
	- 301 - permanent redirect
	- 302 - temporary redirect
	- 304 - not modified
- 4xx - client error
	- 401 - unauthorized error
	- 403 - forbidden error
	- 404 - not found
	- 405 - method not allowed
- 5xx - server error
	- 501 - not implemented
	- 502 - bad gateway
	- 503 - service unavailable
	- 504 - gateway timeout

## http headers
- host = domain name
- content-type / accept = Type of data that's being send or the type of data the receiver can request
- authorization = one method to authenticate users
- cookies / set-cookies = stores data on the user's devices
- user-agent = The device the user is using, LIES a lot tho
- content-security-policy / access-control-allow-origin = provides security features like only allowing specific hosts to make requests

## get and post requests
#### get requests
the parameters will be at the start of the header section
#### post requests
the parameters will be at the end of the body section
eg. sending a form

## session and cookies
#### session
- stored in the server.
- deleted on the browsers on closing it.
- logging in to a website creates a session
#### cookies
- stored in the client's device.
- stays longer even after closing the browser
- enabling "remember me" adds a login cookie, and these cookies can be used to restart it's session stored in the server. 

## Access control
restricting access to specific resource
#### IDORs/ broken access controls
- broken object level authorization (BOLA)
	- accessing an object owned by another user
- broken function level authorization
	- accessing an admin function when logged in as regular user
- missing access control
	- accessing an object when logged out of an account
- cross tenent
	- accessing another tenent object without being a member
# tenants(organization)
- single tenants have multiple org with separate apps to access their respective databases
- multi tenants have a single app to access their databases (problematic)

