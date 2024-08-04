- Types by inference: TypeScript knows the JavaScript language and will generate types for you in many cases. For example in creating a variable and assigning it to a particular value, TypeScript will use the value as its type.
    
    ```tsx
    let x = 'hello world';
    	-> *let x: string*
    ```
    
- We can explicitly describe this object’s shape using an interface declaration:
    
    ```tsx
    interface User {
      name: string;
      id: number;
    }
    
    const user: User = {
      name: "Hayes",
      id: 0,
    };
    ```
    
- There is already a small set of primitive types available in JavaScript: `boolean`, `bigint`, `null`, `number`, `string`, `symbol`, and `undefined`, which you can use in an interface. TypeScript extends this list with a few more, such as `any` (allow anything), [`unknown`](https://www.typescriptlang.org/play#example/unknown-and-never) (ensure someone using this type declares what the type is), [`never`](https://www.typescriptlang.org/play#example/unknown-and-never) (it’s not possible that this type could happen), and `void` (a function which returns `undefined` or has no return value).
- There are two syntaxes for building types: Interfaces and Types. You should prefer `interface`. Use `type` when you need specific features.
- With a union, you can declare that a type could be one of many types. For example, you can describe a `boolean` type as being either `true` or `false`: `type MyBool = true | false;`
- To get the type of a variable, use `typeof`
    
    
    | Type | Predicate |
    | --- | --- |
    | string | typeof s === "string” |
    | number | typeof n === "number” |
    | boolean | typeof b === "boolean” |
    | undefined | typeof undefined === "undefined” |
    | function | typeof f === "function” |
    | array | Array.isArray(a) |
- Generics provide variables to types. Ex: `type numberArray = Array<number>`. Another example:
    
    ```tsx
    interface Backpack<Type> {
      add: (obj: Type) => void;
      get: () => Type;
    }
     
    // This line is a shortcut to tell TypeScript there is a
    // constant called `backpack`, and to not worry about where it came from.
    declare const backpack: Backpack<string>;
     
    // object is a string, because we declared it above as the variable part of Backpack.
    const object = backpack.get();
    ```
    
- Structural type system: if two objects have the same shape, they are considered to be of the same type. The shape-matching only requires a subset of the object’s fields to match.
    
    ```tsx
    interface Point {
      x: number;
      y: number;
    }
     
    function logPoint(p: Point) {
      console.log(`${p.x}, ${p.y}`);
    }
     
    // logs "12, 26"
    const point = { x: 12, y: 26 };
    logPoint(point);
    
    const point3 = { x: 12, y: 26, z: 89 };
    logPoint(point3); // logs "12, 26"
     
    // error here: Argument of type '{ hex: string; }' is not assignable to parameter of type 'Point'.
    const color = { hex: "#187ABF" };
    logPoint(color); 
    ```
    
-