## Understand JSON Data


**JSONP** - Json with Padding
    -    It is used to make cross domain request. While making any request, we need to ensure to add callback method 
         details that should accept JSON response.


### Working with JSON Schema

-   JSON Schema is sort of a blue print that how the data should look like.
-   Created by Internet Engineering Task Force.
-   It is used to validate/verify the JSON Response against the object response we are expecting to recieve 
    without processing. The schema simply validate and throw error in any invalidate data is sent. The 
    validation especifically includes required field or type of the value being passed.
        - Property Name
        - Property Type
        - Required

```

Example Schema :

    var productSchema = {
    "$schema": "http://json-schema.org/draft-04/schema#",
    "id": "http://example.com/schemas/products.json",
    "title": "h+ sport products",
    "description": "schema for h+ sport product data",
    "type": "object",
    "properties": {
        "products": {
        "type": "array",
        "items": {
            "type": "object",
            "properties": {
            "name": {
                "type": "string"
            },
            "image": {
                "type": "string"
            },
            "alt": {
                "type": "string"
            }
            }
        }
        }
    }
    };
```

Example Sample Data on which Schema would be executed.

```


   var productData= {
                "products": [
                    {
                    "image": "vitamin-a.jpg",
                    "alt": "Vitamin A - Product Photo",
                    "name": "Vitamin A"
                    },
                    {
                    "image": "vitamin-bcomplex.jpg",
                    "alt": "B Complex - Product Photo",
                    "name": "B Complex"
                    }
                ]
            }
```

Now to validate the received JSON response against the schema, we used **tv4.mins.js**, which is a java script library called tiny validator, and it would validate the JSON data against defined JSON Schema.

```
//Validate and returns the error when First issue occurs.
//The return would be only first issue details
var productResult = tv4.validate(productData, productSchema);
if(productResult === true) {
    console.log("Valid Data");
} else {
    console.log(tv4.error);
} 

//To get the list of all issues in one run we need to use tv4.validateMultiple instead.
//This returns array list of errors.
var productResult = tv4.validateMultiple(productData, productSchema);
if(productResult === true) {
    console.log("Valid Data");
} else {
    console.log(tv4.error);
} 

```

As we discussed about the schema details in above examples, it really seems a tedious task to generate schema. For that, we can use schema generator which provides us the generated schema for sample json.

To do that, go to (jsonschema.net)[http://jsonschema.net/], and enter sample JSON details in JSON section. Once entered, click on **Generate Schema** to generate schema of JSON. Infact, while genenrating schema, it also shows some option that we can select such as MetaData, Description, Required, Objects, Arrays, Ids etc.