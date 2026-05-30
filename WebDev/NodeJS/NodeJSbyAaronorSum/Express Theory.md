#personal #webdev 

Also see [[Brief Pointers about Expressjs]]

# Routes
Routes are paths on which users can make requests on. Requesting data requires HTTP requests. There are different types of HTTP requests called HTTP verbs. They are indications to the server on the type of operation or request.

The second argument to functions like `.get()` are called route handlers. They are callback functions that have two arguments- _request_ object which has information related to the incoming requests, eg HTTP headers, cookies etc, and the _response_ object which can be used to modify the response before sending it to the user, eg status code, json objects etc.

==It is industry standard to prefix all endpoints with `/api` when building APIs==

# Route params
Route params allow use to pass data dynamically through the route. The value of the route params is always in the form of string hence, we convert them according to different types using `parseInt(<param_value>)`

# Query params
Query string are specified in the following key value pairs structure `.../products?key1=val1&key2=val2`

They are used to either pass information among different pages within the same site or or add additional data to request that we would not send in the body. These key-value pairs are parsed into JSON objects by Express.

# POST requests
These requests enable creation of data that can be later stored in a database. This data is known as payload/request body. Then we perform validation, parsing etc before saving it to a database. Finally, we return the 201 status code.

# PATCH vs PUT requests
PATCH requests update records partially whereas PUT requests are used to completely replace a data resource.

# Middleware
In it's general sense, middleware means a middle process that runs between other processes. In express, the middleware function is also a request handler, therefore it has the `request` and `response` properties as well as an additional `next` which is a function called after the execution of the middleware.

There is no direct way of passing data from one middleware to another, however we can attach them to the request object.

# Validation
The express-validator is used to valid incoming data. Server-side validation is more important than client-side validation since validation on the client-side can be bypassed using other clients like Postman.

# Routers
Routes allow the organization of api endpoints according to domains, eg user domains, product domains etc. 