# TypeScript L&L

## 1. Inference
  ##### Type Annotations and Inference
  1. Type annotations, code we add to tell Typescript what type of value a variable will refer to
  2. Type inference, TypeScript tries to figure out what type of value a variable refers to
  examples,
  ```tsx
  // Type Inference
  let a = "hi"
  a = 1 // typescript will show an warning
  
  // Type Annotations
  // Primitive Types: number, boolean, void, undefined, string, symbol, null
  // Object Types: functions, arrays, classes, objects
  // ex. You assign the type annotation by using colon and the desire type
  ```
  
  ##### Annotations with Variables
  ```tsx
  let apples: number = 5;
  let apples: number = 'hi'; // typescript will show an error
  
  let nothing: undefined = undefined
  let almostNothing: null = null
  
   // Built In Objects
  let now: Date = new Date(); // Date is an internal TypeScript object
  ```
  ##### Object Literal Annotations
  ```tsx
  let colors: string[] = ['red', 'green', 'blue']
  let myNumbers: number[] = [1,2,3]
  let truths: boolean[] = [true, true, false]
  
  // classes
  class Car {
  
  }
  
  let car: Car = new Car();
  
  // object literal (aka object)
  // ex. we assign an object to the variable 'point'
  // with x and y properties that can only be a number type
  
  let point: { x: number; y: number } = {
    x: 10, // if x: 'abc', an error message will appear
    y: 20
  };
  ```
  
  ##### Annotations Around Functions
  ```tsx
  // Function
  // - as developers, we care about what arguments that will go into the function, and what the function will return
  // - annotation is on the left side of equal sign, right hand side is the actual implementation
  
  const logNumber: (i: number) => void = (i) => {
    console.log(i);
  }
  ```
  ##### Understanding Inference
  ```tsx
  // if the "variable declaration" and "variable initialization" are on the same line, TypeScript will look at the type of the "variable initialization" and use that as the type.
  
  const color = 'red'
  
  
  // Type Inference will not work if declaration and initialization are not on the same line
  let apples; // any
  apples = 5;
  
  ```
  
  ##### The `Any` type
  ```tsx
  // 1. any is a type, same as 'string' or 'boolean'
  // 2. means TS has no idea what this is, because it can't check for correct property references
  // 3. avoid variables with 'any' at all cost, because the purpose of TS is to catch errors in our code, if it does not know the type, it cannot do any error checking
  
  // When to use annotations
  // 1) Function that returns the 'any' type
  const json = '{"x": 10, "y": 20}';
  const coordinates = JSON.parse(json); // coordinates and the function are both any
  console.log(coordinates); // {x: 10, y: 20};
  
  coordinates.invalid_method(); // TS is not able to show errors when im calling a property that does not exist, bc the variable 'coordinates' has an 'any' type
  ```
  
  ##### Fixing the `Any` type
  ```tsx
  const coordinates:{ x: number, y: number } = JSON.parse(json);
  
  coordinates.invalid_method(); // TS will now show an error
  
  ```
  
  ##### Delayed Initialization
  ```tsx
  // 2) When we declare a variable on one line and initialize it later
  
  let trees = ['oak', 'pine', 'maple']
  let treeOfCanda: string;
  
  trees.forEach((tree) => {
    if (tree === 'maple'){
      treeOfCanada = 'maple';
    }
  })
  
  ```

  #### When inference doesn't work
  ```tsx
  // 3) Variable whose type cannot be inferred correctly
  let humans = ['Winston', 'Cody', 'Meraj']
  let isAllergicToCucumber: boolean | number = false;
  
  humans.forEach((human)=>{
    if (human === 'Winston'){
      isAllergicToCucumber = 'Winston';
    }
  })
  
  ```
  

## 2. Annotations with Functions and Objects
  ##### More on Annotations Around Functions
  ```tsx
    const add = (a: number, b: number): number => {
      return a + b;
    }
  ```
  ##### Inference around functions
  ```tsx
  // You should always add return annotations for functions
  
  const subtract = (a: number, b: number) => {
    a - b;
  } // we forgot to return here, however TS is not warning us bc of type inference
  
  const subtract = (a: number, b: number): number => {
    return a - b; 
  } // after adding type annotation for the function's return type, TS will now warn us if we did not return the correct type 
  
  ```
  ##### Annotations for Anonymous Functions
  ```tsx
  function divide(a: number, b: number): number {
    return a / b;
  }
  
  const multiply = function(a: number, b: number): number {
    return a * b;
  }
  ```
  
  ##### Void and Never
  ```tsx
  const logger = (message: string): void => {
    console.log(message);
  }
  
  // The never type is used when you are sure that something is never going to occur. 
  // For example, you write a function which will not return to its end point or always throws an exception
  const throwError = (message: string): never => {
    throw new Error(message);
  }
  ```
  ##### Destructuring with Annotations
  ```tsx
  const todaysWeather = {
    date: new Date(),
    weather: 'sunny'
  }
  
  // Before Destructuring
  const logWeather =(todaysWeather: {
    date: Date;
    weather: string;
  }): void => {
    console.log(date);
    console.log(weather);
  }
  
  // After Destructuring
  const logWeather =({
    date,
    weather
  }: {
    date: Date;
    weather: string;
  }): void => {
    console.log(date);
    console.log(weather);
  }
  ```
  
  ##### Annotations Around Objects
  ```tsx
  const profile = {
    name: "alex",
    age: 20,
    coords: {
      lat: 0,
      lng: 15
    },
    setAge(age: number): void {
      this.age = age;
    }
  };

  const { age }: { age: number } = profile;
  const {
    coords: { lat, lng }
  }: { coords: { lat: number; lng: number } } = profile;

  ```

## 3. Typed Arrays?
  ##### Arrays in TypeScript
  ##### Why Typed Array?
  ##### Multiple Types in Arrays
  ##### When to use Typed Arrays (example from FG app?)


## 4. Tuples
  ##### Tuples in TypeScript
  ##### Tuples in Action
  ##### Why Tuples?


## 5. Interface
  ##### Interfaces 
  ##### Long type annotations
  ##### Fixing long type annotations with Interface
  ##### Syntax around Interface
  ##### Functions in Interface
  ##### Code Reuse with Interface
  ##### General Plan with Interface
  ##### What is the ? after a variable or function name?
  ##### Quiz?
  ##### Example in FG app?
  
## 6. Generics
  ##### 
  **

##### example, [https://github.com/BetterTheWorld/flipgive-mobile/commit/8baa1e6cf71281da519d06cabf4d41676ec34253](https://github.com/BetterTheWorld/flipgive-mobile/commit/8baa1e6cf71281da519d06cabf4d41676ec34253)

  #####

**


## 7. Convert a FG JavaScript file to TypeScript
  ##### Teamsnap
  ##### Timeline

## 8. From Cody
  #### Basic types
  #### Typing variables
  #### Typing functions, argument types, function return types
  #### Declaring object types with type and interface, not sure its worth going into the differences but wouldn’t be surprised if someone asks so maybe be prepared to answer
  #### Enums
  ```tsx
  // Enums
  // Allows us to define a set of named constants. Enums can make it easier to document intent, or create a set of distinct 
 cases. By default, TypeScript will define enums as numeric, but we define it mostly with strings
  
  enum Direction {
    Up = 1,
    Down,
    Left,
    Right,
  }
  console.log(Direction.Down)
  // 2
  enum Direction {
    Up = "UP",
    Down = "DOWN",
    Left = "LEFT",
    Right = "RIGHT",
  }
  console.log(Direction.Down)
  // "DOWN"
  ```
  #### Generics
  #### How to type React components
