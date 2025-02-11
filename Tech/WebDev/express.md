## middleware
- middleware are just functions that has access to the request and response objects
- they can end a request-response cycle
- they have access to the next middleware function. Usually the next middleware functions are called "next"
- responce 