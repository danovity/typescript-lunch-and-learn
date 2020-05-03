# TypeScript L&L

## 1. Inference
  ##### Type Annotations and Inference
  Type annotations, code we add to tell Typescript what type of value a variable will refer to
  Type inference, TypeScript tries to figure out what type of value a variable refers to
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
  
  ##### Understanding Inference
  ##### The `Any` type
  ##### Fixing the `Any` type
  ##### Delayed Initialization
  ##### What is Inference?

  ##### When should you not use Inference?

  - What is `any` type?


## 2. Annotations with Functions and Objects
  ##### More on Annotations Around Functions
  ##### Inference around functions
  ##### Annotations for Anonymous Functions
  ##### Void and Never
  ##### Destructuring with Annotations
  ##### Annotations Around Objects


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
