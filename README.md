# TypeScript L&L

## Why use TypeScript?
  ##### 1. Code Suggestions

  TypeScript populates with the options while you type which saves a lot of dev effort of figuring out what should be written. Writing in TypeScript makes it self explanatory. E.g if a new developer joins the team and he is reusing a component, TypeScript will suggest what are the props required in the following screenshot.
  ![image](https://user-images.githubusercontent.com/6895716/81054589-131a8d80-8e95-11ea-8db7-780802cb7fb8.png)
  
  ##### 2. Highlight the errors as early as possible
  
  While you are writing, TypeScript tells you what is wrong.
  ![image](https://user-images.githubusercontent.com/6895716/81054404-c8007a80-8e94-11ea-9610-d170424562de.png)

 
## 1. Type Annotations and Inference
  ##### Type Inference
  ```tsx
  // Type Inference
  // Definition: Type inference, TypeScript tries to figure out what type of value a variable refers to
  let campaign = "FlipGive"
  campaign = 1 // typescript will show an warning
  ```
  ![image](https://user-images.githubusercontent.com/6895716/81054916-ad7ad100-8e95-11ea-99bf-49cc1c28ad20.png)

  
  ##### Type Annotations with Variables
  ```tsx
  // Type Annotations
  // Definition: Type annotations, code we add to tell Typescript what type of value a variable will refer to
  // Primitive Types: number, boolean, void, undefined, string, symbol, null
  // Object Types: functions, arrays, classes, objects
  // ex. You assign the type annotation by using colon and the desire type
  let fundraiser: string = 'Victor';
  let fundraiser: number = 'hi'; // typescript will show an error
  ```
  ![image](https://user-images.githubusercontent.com/6895716/81055204-3b56bc00-8e96-11ea-9397-ce0812ff5b9d.png)

  ```tsx
  let nothing: undefined = undefined // Something hasn't been initialized
  let almostNothing: null = null     // Something is currently unavailable
  
   // Built In Objects
  let now: Date = new Date();        // Date is an internal TypeScript object
  ```
  ##### Object Literal Annotations (aka object)
  ```tsx
  let giftcards: string[] = ['Amazon', 'Walmart', 'Apple']
  let intentIds: number[] = [1,2,3]
  let userHaveJoinedTeam: boolean[] = [true, true, false]
  ```
  ![image](https://user-images.githubusercontent.com/6895716/81056571-c46ef280-8e98-11ea-8b42-a476a6ad2ba4.png)

  ```tsx
  // classes
  class Fundraiser {
    constructor(name: string, email: string){
      name  = 'Sean'
      email = 'sye@flipgive.com'
    };
  }
  
  let sean: Fundraiser = new Fundraiser();
  ```
  ![image](https://user-images.githubusercontent.com/6895716/81056968-8de5a780-8e99-11ea-835c-4513489ea62a.png)

  ```tsx
  // ex. we assign an object to the variable 'point'
  // with x and y properties that can only be a number type
  
  let transaction: { intent_token: string; fundraiser_id: number } = {
    intent_token: 'abc', // if intent_token: 10, an error message will appear
    fundraiser_id: 8
  };
  ```
  ![image](https://user-images.githubusercontent.com/6895716/81057271-182e0b80-8e9a-11ea-9f4c-8dbe9a4afe70.png)

  
  ##### Annotations Around Functions
  ```tsx
  // Function
  // - as developers, we care about what arguments that will go into the function, and what the function will return
  // - annotation is on the left side of equal sign, right hand side is the actual implementation
  
  // Without TS
  const joinTeam = (user_id) => {
    console.log(user_id);
  }
  
  // With TS
  const joinTeam: (user_id: number) => void = (user_id) => {
    console.log(user_id);
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
  
## 5 Interface VS Types
  ##### Are they the same thing? They seem to be doing the same thing.
  Short answer, it doesn't really matter.
  The feature sets of both Interface and Types have become so similar 
  
  
  ##### Interface
  ```tsx
  // Geared towards defining the shape of objects or classes
  // Most of the time, we are using objects (Campaigns, Fundraisers etc)
  // And Interfaces are built deliberately for that.
  
  
  // 1. Implementing an Object
  
  interface Campaign {
    name: string,
    amount_raised: number
  }
  
  const flipgive: Campaign = {
    name: 'FlipGive Giving Club',
    amount_raised: 1000
  }
  
  // If I type in `n1ame`
  // TS will show a warning
  
  const flipgive: Campaign = {
    n1ame: 'FlipGive Giving Club',
    amount_raised: 1000
  }
  
  
  // 2. Functions
  interface LeaveCampaign {
    (name: string): string;
  }
  
  const leftCampaign: LeaveCampaign = (name) => 'FlipGive Giving Club';
  
  // if we assign `name` with Boolean, TS will yell at me
  
  const leftCampaign: LeaveCampaign = (name: boolean) => 'FlipGive Giving Club';
  
  
  // 3. Extends
  interface User {
    name: string;
    email: string;
  }
  interface Fundraiser extends User {
    campaign_id: ID;
  }
  
  // This will show an error because I'm missing a required property
  const fundraiser_1: Fundraiser = {
    name: 'Gerry',
    email: 'gsuwignyo@flipgive.com'
  }
  
  // 4. Declaration Merging (Interface's unique feature)
  // TS allows you to merge these two interfaces
  interface Fundraiser {
    name: string;
    email: string;
  }
  interface Fundraiser {
    campaign_id: ID;
  }
  
  // Again, this will STILL show an error because I'm missing a required property
  // Is this good or bad? We will let the Senior devs decide.
  const fundraiser_1: Fundraiser = {
    name: 'Gerry',
    email: 'gsuwignyo@flipgive.com'
  }
  ```
  
  ##### Type Alias
  **Type aliases**are exactly the same as their original**types**, they are simply alternative names.
  
  ```tsx
  // 1. General Use
  type isFundraiser = boolean;
  
  // Downside of using Type Aliases:
    // warning message is not as descriptive as Interface
    // ex. it will warn me that string 'true' is not assignable to type 'boolean', not type 'isFundraiser', bc 'isFundraiser' is just a boolean
    // side note: this can be achieved by using an Opaque Type, it has been requested but not supported in TS at the moment
    const gerry: isFundraiser = 'true';
    
    
  // 2. Why Type Alias and Interface are very similar now days.
  // Improved error message when using Type Alias to define an object
  
  type Fundraiser = {
    name: string;
    campaign_name: string;
  }
  
  const fundraiser: Fundraiser = {
    name: 'Gerry'
  }
  
  
  // 3. Type Alias will not able to extend
  // why not? bc when an object is defined with Type Alias, the shape is very fixed.
  
  // Method 1: Intersection (As of version 2.7)
  
  type Fundraiser = {
    name: string;
    campaign_name: string;
  } & { amount_raised: number; }
  
  const fundraiser: Fundraiser = {
    name: 'Gerry',
    campaign_name: 'FlipGive'
  } // this will show amount_raised is missing
  
  // Method 2: Union
  
  type Fundraiser = {
    name: string;
    campaign_name: string;
  } 
  
  type User = {
    amount_raised: number;
  }
  
  type Gerry = Fundraiser | User;
  
  const gerry: Gerry = {
    name: 'Gerry',
    campaign_name: 'FlipGive'
  }
  
  ```
  
  ##### Rule of Thumb When Using Type Aliases vs Interface 
  [Advanced Types · TypeScript](https://www.typescriptlang.org/docs/handbook/advanced-types.html)
  
  1. Because[an ideal property of software is being open to extension](https://en.wikipedia.org/wiki/Open/closed_principle), you should always use an interface over a type alias if possible.
  2. On the other hand, if you can’t express some shape with an interface and you need to use a union or tuple type, type aliases are usually the way to go.

  
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
