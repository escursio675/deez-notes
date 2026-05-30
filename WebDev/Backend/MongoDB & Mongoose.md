#webdev 

# Mongoose

## Creating a model

A model in mongoDB is an interface that is used to interact with the database through functions like `.create()`, `.findOne()` etc.

```
import mongoose from 'mongoose';

const urlSchema = new mongoose.Schema(
{
	shortCode: {
		type: String,
		required: true,
		unique: true,
		index: true

	},
	longCode: {
		type: String,
		required: true,
	}
},
{timestamps: true}
); 

const Url = mongoose.model('Url', urlSchema);
export default Url;
```

## .create()
`const <value> = await mongoDBmodel.create({...});` returns the created mongoDB document.