#personal #webdev 

Also see [[Express Theory]]

# Setup
1. `npm init -y` to initialize a dir as an npm repository and generate a `package.json` file.
2. `npm i express` to install ExpressJS
3. `npm i -D nodemon` to be able to run applications in watch mode
4. Define `"start:dev" : "nodemon ./src/index.js"` under `"scripts"`
5. Define `"start": "node ./src/index.js"` to run in production setting
6. Define new property `"type": "module"` to use ESM. Change the file extensions to `.mjs`
# Basic Boilerplate
```
import express from "express";

const app = express();
const PORT = process.env.PORT || 3000;

app.listen(PORT, () =>{
	console.log(`Running on port ${PORT}`);
})
```
Here `process` is a global with object `env` which holds environment variables.

# Running the server
`npm run start:dev` to run in watch mode.

# Route Basics

```
app.get('/', (request, response) =>{
	response.send("Hello world!");
	//OR
	response.status(200).send({msg: "Hello World!"});
});

app.get('/api/users', (request, response) =>{
	response.send([
		{id: 1, username: "jason", displayName: "JASON"},
		{id: 1, username: "jason", displayName: "JASON"},
		{id: 1, username: "jason", displayName: "JASON"}
	]);
});

app.get('/api/products', (request, response) =>{
	response.send([
	{id: 123, name: "phone", price: 20000},
	{id: 123, name: "phone", price: 20000},
	{id: 123, name: "phone", price: 20000}
	]);
});
```

# Route Params
```
const mockUsers = [
	{id: 1, username: "jason", displayName: "JASON"},
	{id: 1, username: "jason", displayName: "JASON"},
	{id: 1, username: "jason", displayName: "JASON"}
];


app.get('/api/users', (request, response) =>{
	response.send(mockUsers);
});

app.get('/api/users/:id', (request, response) =>{
	console.log(request.params.id);
	const parsedId = parseInt(request.params.id);
	
	if(isNaN(parsedId))
		return response.status(400).send({msg: " Bad Request"});		
	// 400 => Bad Request
	
	const findUser = mockUsers.find(
	(user) => user.id === parsedId
	)
	
	if(!findUser)
		return response.sendStatus(400);
	
	return response.send(findUser);
});

```
In the above case, if the user provides no ID, the '/api/users' route handler will be called.

# Query params
```
app.get('/api/users', (request, response) => {
	console.log(request.query);
	
	const { query: {filter, value} } = request;
	//destructure query from request and further destructure filter and value from query
	
	if(filter && value)
		return response.send(
			mockUsers.filter((user) => user[filter].includes(value));
		);
	
	//when query values are undefined
	return response.send(mockUsers);
});
```

# POST requests
```
app.post('/api/users', (request, response) =>{
	console.log(request.body);
	
	//assuming the request body is valid
	const { body } = request;
	const newUser = [ id: 8, ...body];
	mockUsers.push(newUser);
	
	return response.status(201).send(newUser);
});
```
The above can be differentiated with the `app.get()` request by the request type/http verb.

Request body can be logged as 'undefined' because by default express does not parse the request bodies. This can be done through middlewares.

==middleware are functions that are called before certain api requests are handled==

```
const app = express();

app.use(express.json());
```

# PUT requests
```
app.put('/api/users/:id', (request, response) =>{
	const { body, params: {id} } = request;
	
	const parsedId = parseInt(id);
	if(isNaN(parsedId))
		return response.sendStatus(400);
		
	const findUserIndex = mockUsers.findIndex(
	(user) => user.id === parsedId;
	);
	
	//findIndex() returns -1 if not found
	if(findUserIndex === -1)
		return response.sendStatus(404);
		
	//since using PUT, update the entire record
	mockUsers[findUserIndex] = {id: parsedId, ...body};
	
	return response.sendStatus(200);
});
```

# PATCH requests
```
app.patch('/api/users/:id', (request, response) => {
	const { body, params: {id} } = request;
	
	const parsedId = parseInt(id);
	if(isNaN(parsedId))
		return response.sendStatus(400);
		
	const findUserIndex = mockUsers.findIndex(
	(user) => user.id === parsedId;
	);
	
	if(findUserIndex === -1)
		return response.sendStatus(404);
		
	mockUsers[findUserIndex] = 
	{ 
		...mockUsers[findUserIndex], ...body
	};
	
	return response.sendStatus(200);
});
```

# DELETE requests
```
app.delete('/api/users/:id', (request, response) =>{
	const { params: {id} } = request;
	// OR const { id } = request.params;
	
	const parsedId = parseInt(id);
	
	if(isNaN(parsedId))
		return request.sendStatus(400);
		
	const findUserIndex = mockUsers.findIndex(
	(user) => user.id === parsedId
	);
	
	if(findUserIndex === -1)
		return response.sendStatus(404);
	
	mockUsers.splice(findUserIndex, 1);
	return respnse.sendStatus(200);
});
```

# Middlewares
```
app.use(express.json());

const loggingMiddleware = (request, response, next) => {
	console.log(`${request.method} - ${request.url});
	
	next();
};

//use the middleware globally
app.use(loggingMiddelware, middleware2, ...);

//user for certain endpoints
app.get('/', loggingMiddleware, (request, response) =>{
	response.send("Hello world!");
});

```

Alternative syntax for route specific middlewares
```
app.get('/', 
(request, response, next) =>{
	console.log("Base URL")
	next();
},
(request, response, next) =>{
	console.log("Base URL 2")
	next();
}, 
(request, response) =>{
	response.send("Hello world!");
});
```

==Middlewares must be registered before calling the route methods in which they are used.==

==next can be used along normal request methods as well ie, `app.get('/', (request, response, next) => {...})`==

## Middleware Application
Middlewares can be used to make reusable logic that can be used in request method, eg, the validation of user logic as seen before

```
const resolveIndexByUserId = (request, response, next) =>{
	const { body, params: {id} } = request;
	
	const parsedId = parseInt(id);
	if(isNaN(parsedId))
		return response.sendStatus(400);
		
	const findUserIndex = mockUsers.findIndex(
	(user) => user.id === parsedId;
	);
	
	if(findUserIndex === -1)
		return response.sendStatus(404);
		
	response.findUserIndex = findUserIndex;
	next();
};
```

and then use
```
app.patch('/api/users/:id', resolveIndexByUserId, 
(request, response) => {

	const { body, findUserIndex } = request;
		
	mockUsers[findUserIndex] = 
	{ 
		...mockUsers[findUserIndex], ...body
	};
	
	return response.sendStatus(200);
});
```

==There is no direct way of passing data from one middleware to another, however we can attach them to the request object==

To attach a data property to the request object, we perform the attachment on an earlier middleware.

# Validation
## Setup
`npm install express-validator`

## Query parameters
```
//used to validate query parameters
import { query, validationResult } from "express-validator";

app.get('/api/users',
query('filter')
	.notEmpty()
	.isLength({min: 3, max: 10})
	.withMessage("Must be between 3 and 10 chars"), 
	//sets error message for previous validator
(request, response) =>{
	//extract the validation errors
	const result = vlidationResult(request);
	...
});
```

The validation function returns an instance of validation chain which can further be used for performing other validations. The validation functions do not throw actual errors. However they do attach the errors in the response body.

## Request bodies
```
import { query, validationResult, body, matchedData } from "express-validator";

app.post('/api/users',
	body().('username')
	.notEmpty()
	.withMessage("Username cannot be empty")
	.isLength(min: 5, max: 32)
	.withMessage("Username must be 5 to 32 chars")
	.isString()
	.withMessage("Username must be a string"),
	(request, response) =>{
	
	const result = validationResult(request);
	console.log(result);
	
	if(!result.isEmpty())
		return response.status(400)
		.send({errors: result.array()});
	
	const data = matchedData(request);
	
	
	const newUser = [ id: 8, ...data];
	mockUsers.push(newUser);
	
	return response.status(201).send(newUser);
});

```

`matchedData()` is used to obtain the validated data.

## Using schema
Schemas are objects that have a set of validators defined that can be reused/used to clean up the validation code from a route method.

utils/validationSchemas.js
```
export const createUsersValidationSchema = {
	username: [
	isLength: {
		options:{
			min: 5,
			max: 32
		},
		errorMessage: "Username must be 5 to 32 chars long"
	},
	notEmpty: {
		errorMessage: "Username cannot be empty"
	},
	isString: true,
	],
	
	displayName: {
		notEmpty: true
	}
};
```

then use as
```
import { query, validationResult, body, matchedData, checkSchema } from "express-validator";

import { checkUserValidationSchema } from 'utils/validationSchemas.js'

app.post('/api/users',
	checkSchema(checkUserValidationSchema),
	(request, response) =>{
	
	const result = validationResult(request);
	console.log(result);
	
	if(!result.isEmpty())
		return response.status(400)
		.send({errors: result.array()});
	
	const data = matchedData(request);
	
	
	const newUser = [ id: 8, ...data];
	mockUsers.push(newUser);
	
	return response.status(201).send(newUser);
});
```

# Routers

src/routes/users.mjs
```
import { query, validationResult, body, matchedData, checkSchema } from "express-validator";

import { checkUserValidationSchema } from 'utils/validationSchemas.js'

import { Router } from "express";
const router = Router();

router.get('/api/users',
	checkSchema(checkUserValidationSchema),
	(request, response) =>{
	...
	}
);

export default router;
```

then use:
```
imoprt userRouter from "/routes/users.msj"

app.use(userRouter);
```

Use another index.mjs file as routes/index.mjs to import the multiple routes

``` 
import { Router } from "express";
imoprt userRouter from "/users.mjs";
imoprt productsRouter from "/products.mjs";

const router = Router();

router.use(userRouter);
router.use(productsRouter);

export default router;
```

index.msj
```
import routes from '/routes/index.mjs';

app.use(routes);
```

Middlewares can also be used in this method.


# Databases
## Setup
1. `npm i mongoose`

## Basic Boilerplate

```
import mongoose from "mongoose";

//'express_tutorial is the database
mongoose.connect('mongodb://localhost/express_tutorial')
.then(() => console.log("Connected to database"))
.catch((err) => console.log(`Error: ${err}`));

```

The default port of mongoose is 27017. The `.connect()` method returns a Promise.

mongoose/schema/user.js
```
import mongoose from "mongoose";

const UserSchema = new mongoose.Schema([
	username: {
		type: mongoose.Schema.Types.String,
		required: true,
		unique: true,
	}
	displayName: mongoose.Schema.Types.String,
	password: mongoose.Schema.Types.String,
]);

//compile to a model
export const User = mongoose.model("User", schema);
```

routes/users.mjs
```
import { User } from "/mongoose/schemas/user.njs";
 
	router.post("/api/users",
		checkSchema(checkUserValidationSchema),
		async (request, response) =>{
		
		const result = validationResult(request);
		
		if(!result.isEmpty())
			return response.status(400).send(result.array);
			
		const data = matchedData(request);
		
		const { body } = request;
		cont newUser = new User(body);
		try{
			const savedUser = await newUser.save();
			return response.status(201).send(savedUser);
		} catch(err){
			console.log(err);
			return response.sendStats(401);
		}
	})
```

20:39(Passport.js authentication)