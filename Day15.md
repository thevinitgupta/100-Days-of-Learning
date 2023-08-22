# Typescript Day -3 : Horrors of `any` and working with `ESLint`
`any` is like a fallback datatype in Typescript. But it comes with its issues. 

> Any is a kind of "wild card" type which stands for whatever type.
> Things become implicitly any type quite often when one forgets to type functions.

## Request and Response
While creating an express server, if don't specify the exact type, the `body field is expressed as any` and the same is true for `request.query`. 
But this might cause problems when using this data in real functions. And even if we disallow ❌ `implicit-any using eslint configuration`, typescript does not show errors for the above. 
### Why?
Because the `body` and`Request.query` fields are `explicitly` defined as `any`.
To prevent this, we can do the following : 
- Install `eslint` plugins :
  ```js
  npm install --save-dev eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser
  ```
- Add a file `.eslintrc` and put the following configuration :
```js
{
  "parser": "@typescript-eslint/parser",
  "parserOptions": {
    "ecmaVersion": 11,
    "sourceType": "module"
  },
  "plugins": ["@typescript-eslint"],
  "rules": {

    "@typescript-eslint/no-explicit-any": 2
  }
}
```
Now, the use of `explicit-any` also shows errors.

But there is another problem here.

> What if we actually don't know the type, and can only perform validations? There is a trick :
#### 💡 Turn of `eslint` for a particular property for a single line :
```js
  // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
  const { value1, value2, op } = req.body;
```

## Type Assertion
Using a type assertion is another *dirty trick 🚩*  that can be done to keep TypeScript compiler and Eslint quiet.
If we create a type and assert an incoming variable as that type, it works(with some exceptions).
```js
type Operation = 'multiply' | 'add' | 'divide';
app.post('/calculate', (req, res) => {
  // eslint-disable-next-line @typescript-eslint/no-unsafe-assignment
  const { value1, value2, op } = req.body;

  // validate the data here

  // assert the type
  const operation = op as Operation;
```
> 🚨 Using a type assertion (or quieting an Eslint rule) is always a bit risky thing. It leaves the TypeScript compiler off the hook, the compiler just trusts that we as developers know what we are doing. `If the asserted type does not have the right kind of value`, the result will be a `runtime error`, so one must be pretty careful when validating the data if a type assertion is used.

