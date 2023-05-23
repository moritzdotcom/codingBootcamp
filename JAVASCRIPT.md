# Javascript

The language we will use to build our Application is Javascript. Besides being the most popular language, JS is a good choice for beginners because it is easy to learn and can be used for both frontend and backend development.

## Getting started

To start playing around with JS, we can start a node REPL. REPL stands for Read-Eval-Print-Loop. It is a program that takes input, evaluates it, and returns the result to the user. It is a great way to try out new things and learn a new language.

To start the REPL, we can run `node` in our terminal. We can then write JS code and see the result immediately.

## Variables

Variables are used to store text, numbers or more complex data. By using variables, we can reuse data and make our code more readable.

```js
// We can declare a variable using the const keyword
const name = 'Sebi'; // Name cant be changed

// We can also use let to declare a variable
let age = 30;

// We can change the value of a variable
age = 31;
```

## Data types

There are 7 primitive data types in Javascript:

- String
- Number
- BigInt
- Boolean
- Null
- Undefined
- Symbol

```js
// strings are used to store text
const name = 'Sebi';

// numbers are used to store numbers
const age = 30;

// booleans are used to store true or false
const isCool = true;

// null is used to indicate that a variable is empty
const nothing = null;

// undefined is used to indicate that a variable has not been assigned a value
let something; // By default, variables are undefined
```

Adding to this, we can also use Objects and Arrays to store more complex data.

```js
// Objects are used to store data in key-value pairs
const person = {
  name: 'Sebi',
  age: 30,
};

// We can use dot notation to access the values
console.log(person.name);

// Arrays are used to store lists of data
const fruits = ['apple', 'banana', 'orange'];

// We can use bracket notation to access the values
console.log(fruits[0]);
```

## Functions

Functions are used to group code that belongs together. They can be used to avoid repeating code and make our code more readable.

```js
// We can declare a function using the function keyword
function sayHello() {
  console.log('Hello');
}

// We can call the function like this
sayHello();

// We can also pass arguments to the function
function sayHello(name) {
  console.log(`Hello ${name}`);
}

sayHello('Sebi');
```

## Conditionals

Conditionals are used to execute code based on a condition. We use comparison operators, like `==`, `!==`, `>`, `<`, to compare values.

```js
// We can use if statements to execute code if a condition is true
function sellBeer(age) {
  if (age >= 18) {
    console.log('Here is your beer');
  }
}

// We can use else if to execute code if the first condition is false and the second condition is true
function sellBeer(age, country) {
  if (age >= 18) {
    console.log('Here is your beer');
  } else if (age >= 16 && country === 'Germany') {
    console.log('Here is your beer');
  }
}

// We can use else to execute code if all conditions are false
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

## Objects and arrays

When developing a Web Application, we will often have to work with data. We can use Objects and Arrays to store this data. When we want to display listed jobs, those will be in an array. When we want to display a single job, that will be an object. That said, the jobs we receive from the server might look something like this:

```js
const jobs = [
  {
    id: 1,
    title: 'Frontend Developer',
    company: 'Google',
    location: 'Berlin',
    salary: 50000,
    tags: ['frontend', 'react', 'javascript'],
  },
  {
    id: 2,
    title: 'Backend Developer',
    company: 'Facebook',
    location: 'Berlin',
    salary: 60000,
    tags: ['backend', 'node', 'javascript'],
  },
];
```

Here we have an array ob `job` objects. Each job has an id, title, company, location, salary and tags. All jobs are grouped inside an array. Let's say we would like to change the title of the first job. We can do that like this:

```js
jobs[0].title = 'Fullstack Developer';
```

We can also add a new job to the array with the `push` method:

```js
jobs.push({
  id: 3,
  title: 'Fullstack Developer',
  company: 'Amazon',
  location: 'Berlin',
  salary: 70000,
  tags: ['fullstack', 'node', 'react', 'javascript'],
});
```

Now lets imagine we would like to reduce the salary of each job by 10% to account for our commission. We can do that like this:

```js
jobs.forEach((job) => {
  job.salary = job.salary * 0.9;
});
```

The `forEach` method is used to loop over an array. It takes a function as an argument. This function will be called for each item in the array. The item will be passed as an argument to the function. We can then access the salary of the job and reduce it by 10%.

Let's say we want to keep the old jobs unchanged and create a new array with the reduced salaries. We can do that with the `map` method:

```js
const jobsWithReducedSalary = jobs.map((job) => {
  return {
    ...job,
    salary: job.salary * 0.9,
  };
});
```

In case we want to find a specific job, we can use the `find` method:

```js
const firstJob = jobs.find((job) => job.id === 1);
```

And if we want to get all jobs in Berlin, we can use the `filter` method:

```js
const jobsInBerlin = jobs.filter((job) => job.location === 'Berlin');
```

## Async

When we are working with data, we will often have to wait for the data to be fetched from the server. This is called an asynchronous operation. We can use the `async` and `await` keywords to make our code wait for the data to be fetched.

```js
// We can use the async keyword to declare a function as asynchronous
async function getJobs() {
  // We can use the await keyword to wait for the data to be fetched
  const response = await fetch('https://example.com/jobs');

  // We can then use the response
  const jobs = await response.json();

  // We can then use the jobs
  return jobs;
}
```

Async functions return a `Promise`, which is a fancy word to say that the function will return a value in the future. We can use the `then` method to access the value:

```js
getJobs().then((jobs) => {
  console.log(jobs);
});
```

In case something goes wrong, we can use the `catch` method to handle the error:

```js
getJobs()
  .then((jobs) => {
    console.log(jobs);
  })
  .catch((error) => {
    console.log(error);
  });
```
