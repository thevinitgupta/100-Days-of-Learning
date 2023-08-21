# Typescript Day 2 : Diving more into Types ad Setup with Express
Continuing my journey with `typescript`, I have learnt about the various types and basic usage with `express` to develop simple servers. I also got to explore the various `types` packages that are defined for typescript based development. 

## Production vs. Development Compilation
In production, TypeScript compiles to JavaScript in a separate folder. In development, real-time compilation and auto-reloading help preview changes faster.

## Getting Started
Use the npm package `ts-node` for quick TypeScript execution. Install globally with:

```js
npm install -g ts-node typescript
```

Or install locally for projects with:

```js
npm install --save-dev ts-node typescript
```

### tsconfig.json

It defines how TypeScript interprets the code. Start with basic options like noImplicitAny to enhance type checking.
Type Safety

TypeScript enforces specific types for inputs, aiding in error prevention and editor-level assistance. Create types using the type keyword.

### Return Type
Specify return types to ensure function behavior. Handle possible division by zero errors.

### Unknown Type
unknown is flexible but needs narrowing for operations. It's not assignable to any without assertions.

### Types for Packages
Find @types on npm for package types. Install with:
```js
npm install --save-dev @types/package-name
```

### Generics and Configuration
Utilize "generics syntax" and set configurations in tsconfig.json to shape your TypeScript environment.

### Unused Variables
Handle unused variables with care. Prefixing with underscores can signal intent to the compiler.

### Best Practices
Use import for module importing and adjust noUnusedParameters considering library-wide functions.

### `ts-node-dev`
Consider using ts-node-dev for running your app during development. Install it using `npm` and then configure the script to use ts-node-dev using the following : 
```js
"scripts": {
    "ts-node": "ts-node",
    "start": "ts-node-dev index.ts"
  },
```
A simple server with typescript and express js that returns BMI : 
```js
import express from "express";
import { Request, Response } from 'express';
const app = express();

// test endpoint
app.get("/", (_req ,res)=>{
    res.send("<h1>PONG🤘🚀</h1>");
})
// test endpoint
app.get("/hello", (_req ,res)=>{
    res.send("<h1>Hello, Full Stack!🤘🚀</h1>");
})
// interfaces
interface ReqParams {
  /* Add something as needed */
}
interface ReqBody {
  /* Add something as needed */
}
interface Resbody {
  /* Add something as needed */
}
interface ReqQuery{
    height : number;
    weight : number;
}
type bmiData = "Underweight" | "Normal range" | "Overweight";
const bmiResult = (weight : number, height : number) : bmiData=>{
    const bmi : number = weight/(height*height);
    if(bmi<=18.4){
        return "Underweight";
    }
    else if(bmi>=18.5 &&  bmi<=24.9){
        return "Normal range";
    }
 	else return "Overweight";
}
app.get("/bmi", (req : Request<ReqParams, ReqBody, Resbody, ReqQuery>,res : Response)=>{
    const {height, weight} = req.query;
    if(isNaN(height) || isNaN(weight)){
        res.status(301).json({
            error : "Misformatted parameters"
        })
    }
    res.status(200).json({
        height,
        weight,
        bmi : bmiResult(weight,height/100)
    });
})
const PORT = 5000;
app.listen(PORT, ()=>{
    console.log("App listening on port : ",PORT);
})
```
I'm excited to explore more about TypeScript's dynamic power!
