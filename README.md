# Oxygen

- A programming language designed to be easy to use, and with high safety and performance.
    - It transpiles to Rust/ C/ C++, etc...

## Declarations

- Oxygen has 3 types of Declaration:
    - Constant declaration.

    ```c
        const num1: int = 5                 //Type annotation can be explicitly declared.
        const num2 = 5                      //Types are inferred, so no type annotation is required.
    ```

    - Immutable Variable declaration.
        - By default, all variables are immutable.

    ```js
        var v1: str = "I am a string!"      //Type annotation can be explicitly declared.
        var v2 = "I am also a string!"      //Types are inferred, so no type annotation is required.
    ```

    - Mutable Variable declaration.

    ```rust
        mut m1: str = "I am a string!"      //Type annotation can be explicitly declared.
        mut v2 = "I am also a string!"      //Types are inferred, so no type annotation is required.
    ```

PS: Declare a comment with `//`!

## Import

- You can import code/libraries that you have installed with the `use` keyword!

    ```rust
        use stdlib                          //Importing the standard library.
        use "./lib/lib.oxy"                 //Importing an Oxygen library.
        use json/deserialize                //Import a library module
    ```

## Functions

- There are 2 ways to declare a function:
    - Standard Function Declaration.

    ```rs
        fn function() -> str:               //Unlike variables and constants, you have to explicitly state the return type.
            return "I'm a function!"        
    ```

    ```rs
        fn greet(name: str) -> str:
            return "Hi there, {name}"       //Strings are interpolated!
    ```

    ```rs
        fn no_return(name: str) -> str:
            "Hi there, {name}"              //By default, the last value in the function is returned if no `return` keyword are found.
    ```

    ```rs
        fn void():
            // I do not return anything as I have not been given a return type.
    ```

        - Anonymous Function Declaration.

    ```c
        const func = |x: int| {
            x + 1
        }
    ```

## Data types

- Scalar types:
    - String:
        - Keyword: `str`.
        - Stores an sequences of Characters.
    - Integer:
        - Keyword: `int`.
        - Stores a 64-bit integer.
    - Floating-point number:
        - Keyword: `flt`.
        - Stores a double-precision floating-point number.
    - Boolean:
        - Keyword: `bol`.
        - Stores 2 possible values: `true` or `false`.
    - Character:
        - Keyword: `chr`.
        - Contains a valid UTF-8 character.
    - Any:
        - Keyword: `any`.
        - Cannot be directly used. Represents a group of types.
            - The types can be restricted with Traits.
            - Examples:
                - `any<Numerical>` represents any types with the `Numerical` trait implemented (eg: `int`, `flt`, etc...).
                - `any<Iterable, PartialEq>` represents any types with the `Iterable` and `PartialEq` traits implemented (eg: `str`,  etc...).
- Compound types:
    - Tuple:
        - A tuple is a general way of grouping together a number of values with a variety of types into one compound type. Tuples have a fixed length: once declared, they cannot grow or shrink in size.

    ```js
        var tup: (int, bol) = (69420, true)
    ```

    - Array:
        - An array is a way of grouping together a number of values with the same type into one compound type.
        - Index starts at 0.

    ```js
        var arr = [0, 1, 2, 3, 4, 5]
        arr.append(6)
        print(arr)
        // [0, 1, 2, 3, 4, 5, 6]
    ```

    ```js
        var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        var arr2 = arr[2..7]                //This returns a slice of the original array.
        print(arr2)
        // [2, 3, 4, 5, 6, 7]               
    ```

- Defined Types:
    - Enum:
        - Keyword: `enum`.
        - Define a set of possible values.

        ```rs
            enum Status:
                OK
                FAILED
        ```

        ```rs
            enum Result:
                SUCCESS(any)
                FAILURE(any<Error>)
        ```

        - Match case:
            - Keyword: `match`.

            ```rs
                match Status:
                    case OK:
                        //DO SOMETHING IN CASE OF SUCCESS
                    case FAILED:
                        //DO SOMETHING IN CASE OF FAILURE
            ```

    - Struct:
        - Keyword: `struct`.
        - Structs are similar to tuples, in that both hold multiple related values. Like tuples, the pieces of a struct can be different types. Unlike with tuples, in a struct you’ll name each piece of data so it’s clear what the values mean. Adding these names means that structs are more flexible than tuples: you don’t have to rely on the order of the data to specify or access the values of an instance.

        ```py
            struct Human:
                name: str
                age: int
        ```

## Object-oriented Programming Features

- Traits: Define shared behaviours.
    - Defining a trait:

    ```rs
        trait PartialEq<T: Self>:
            fn eq(self, other: T) -> bol
            fn ne(self, other: T) -> bol
    ```

    - Implementing trait for a data structure/ an enum:

    ```rs
        struct Data:
            val: str
        impl PartialEq for Data:
            fn eq(self, other: T) -> bol:
                self.val == other.val
            fn ne(self, other: T) -> bol:
                self.val != other.val
    ```

    - Traits can be used as a return type, where any types that implement that specific trait can be returned.

    ```rs
        trait UserTrait:
            //Trait content
        fn get_user() -> T<UserTrait>:
            //Function content
    ```
