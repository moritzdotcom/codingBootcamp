# Typescript

Javascript is like jumping out of a plane without a parachute. Typescript adds an additional layer of safety. Besides typesafety, we also get the added benefit of autocompletion when developing and better understanding of our code.

Let me explain the value of Typescript on the `sellBeer` example from the previous section:

```ts
function sellBeer(age, country) {
  if (age >= 18) {
    console.log('Here is your beer');
  } else if (age >= 16 && country === 'Germany') {
    console.log('Here is your beer');
  } else {
    console.log('You are too young');
  }
}
```

In Javascript, you could pass any value to the `sellBeer` function. For example, you could pass a string as the `age` argument. This would result in an error. Those errors are often hard to find and can cause a lot of problems. Let's see how we can prevent this with Typescript:

```ts
function sellBeer(age: number, country: string) {
  if (age >= 18) {
    console.log('Here is your beer');
  } else if (age >= 16 && country === 'Germany') {
    console.log('Here is your beer');
  } else {
    console.log('You are too young');
  }
}
```

Much better! Now we ensure the correct types. We could even define a list of possible countries so we know that the `country` argument will always be a valid country:

```ts
type Country = 'Germany' | 'France' | 'Italy';

function sellBeer(age: number, country: Country) {
  if (age >= 18) {
    console.log('Here is your beer');
  } else if (age >= 16 && country === 'Germany') {
    console.log('Here is your beer');
  } else {
    console.log('You are too young');
  }
}
```

## Types

Typescript has a lot of built-in types. Here are some of the most important ones:

```ts
// We can use the any type to allow any value
let anyValue: any = 'Hello';

// We can use the number type to allow numbers
let numberValue: number = 42;

// We can use the string type to allow strings
let stringValue: string = 'Hello';

// We can use the boolean type to allow booleans
let booleanValue: boolean = true;

// We can use the object type to allow objects
let objectValue: object = { name: 'Sebi' };

// We can use the array type to allow arrays
let arrayValue: string[] = ['Hello', 'World'];

// We can use the tuple type to allow arrays with a fixed length
let tupleValue: [string, number] = ['Hello', 42];

// We can use the function type to allow functions
let functionValue: () => void = () => console.log('Hello');

// We can use the null type to allow null
let nullValue: null = null;

// We can use the undefined type to allow undefined
let undefinedValue: undefined = undefined;
```

## Interfaces

We can use interfaces to define the shape of an object. For example, we could define the shape of a job like this:

```ts
interface Job {
  id: number;
  title: string;
  description: string;
  salary: number;
  location: string;
  company: string;
  tags: string[];
}
```

We can then use this interface to define the shape of our jobs:

```ts
const jobs: Job[] = [
  {
    id: 1,
    title: 'Frontend Developer',
    description: 'Lorem ipsum',
    salary: 50000,
    location: 'Berlin',
    company: 'Google',
    tags: ['frontend', 'react', 'javascript'],
  },
  {
    id: 2,
    title: 'Backend Developer',
    description: 'Lorem ipsum',
    salary: 60000,
    location: 'Berlin',
    company: 'Google',
    tags: ['backend', 'node', 'javascript'],
  },
];
```
