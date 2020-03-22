## ThereforeJS

A small and easy-to-integrate JavaScript library for managing errors.

- Write shorter, simpler functions
- Improve the testability of your code
- Provide a variety of fallback scenarios if an error occurs

![](https://i.kym-cdn.com/photos/images/original/000/343/462/79a.gif)

### Setup

- Instantiate the class
- Prepare a config object
- Wrap your function call in an IAm method

```
let iam = new IAm();

let config = {
  // tell me what to do if there's an error, or just give me some defaults
}

function thisMightNotWork () {
  // do something that might throw an error
}

In the flow of your logic in your code:

function thisDoesSomething () {
  let someValue = iam.watching(thisMightNotWork, config)
}
```

### Available Methods
- `watching()`: Provides a try/catch/finally block. Accepts a callback function and a config object as arguments.

You can pass a config in as a global config during the IAm class instantiation or just provide a config each time you wrap a callback. All of these properties in the config object below are optional.
```
let config = {
  try: {
    default: *any*,
    execute: *Function*
  },
  catch: {
    default: *any*,
    execute: *Function*,
    logType: *string*, // a console method that outputs the error to the console (e.g. 'log', 'error', 'warn')
    provideErr: *boolean*
  },
  finally: {
    default: *any*,
    execute: *Function*
  },
  silence: *boolean* // prevent all console logs generated by IAm
}
```

Here's the order in which a value is returned from a call to `watching()`:
```
1. value returned from finally: execute
2. finally: default
3. [if no error] value returned from the callback argument provided to watching()
4. [if no error] value returned from try: execute
5. [if no error] try: default
6. value returned from catch: execute
7. catch: provideErr
8. catch: default
```