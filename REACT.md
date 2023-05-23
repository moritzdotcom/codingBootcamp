# React

React is a Javascript library for building user interfaces. React can be used as a base in the development of single-page or mobile applications. It embraces a component-based approach to building applications. That means we split our App into small components that can be reused and combined to build complex user interfaces. A Button could be a component, a Navbar could be a component, a Card could be a component, and so on.

## Example React File

As a starting point we can look at a simple React file:

```jsx
export default function App() {
  return (
    <div>
      <h1>Hello this is my App</h1>
    </div>
  );
}
```

Now let's add a Call to action button:

```jsx
export default function App() {
  return (
    <div>
      <h1>Hello this is my App</h1>
      <button onClick={() => alert('I was clicked')}>Click me!</button>
    </div>
  );
}
```

And make that button its own component:

```jsx
function Button() {
  return <button onClick={() => alert('I was clicked')}>Click me!</button>;
}

export default function App() {
  return (
    <div>
      <h1>Hello this is my App</h1>
      <Button />
    </div>
  );
}
```

By splitting our App into small components we can reuse them and combine them to build complex user interfaces.

## Props

Now we have a button component, but it will always look the same. What if we want to use the button for different things like a login button? We can do this by passing props to the button component.

```tsx
interface ButtonProps {
  label: string;
}

export default function Button({ label }: ButtonProps) {
  return <button>{label}</button>;
}
```

We defined a parameter for the button component called `label`. Now we can use the button component like this:

```tsx
<Button label="Sign up" />
<Button label="Login" />
```

One special prop in React is the `children` prop. This prop contains the content between the opening and closing tag of the component. We can use this prop to pass content to the button component.

```tsx
interface ButtonProps {
  children: React.ReactNode;
}

export default function Button({ children }: ButtonProps) {
  return <button>{children}</button>;
}
```

Now we can use the button component like this:

```tsx
<Button>Sign up</Button>
<Button>Login</Button>
```

To tell the button what it should do when it is clicked, we can pass a function as a prop. In case we don't want the button to do anything when it is clicked, we can define the `onClick` prop as optional using a `?`:

```tsx
interface ButtonProps {
  onClick?: () => void;
  children: React.ReactNode;
}

export default function Button({ onClick, children }: ButtonProps) {
  return <button onClick={onClick}>{children}</button>;
}
```

Now we can use the button component like this:

```tsx
<Button onClick={() => console.log('Clicked!')}>Sign up</Button>
```

## State

State is a way to store data in React. We can use state to store data that changes over time. For example, we can use state to store the current user, the current page, or the current theme. We can use state to store any data that changes over time.

For example, if we wanted to store and display the count of how often a button was clicked, we could modify our Button component like this:

```jsx
function Button() {
  const [count, setCount] = useState(0);

  return (
    <button onClick={() => setCount((c) => c + 1)}>
      I was clicked {count} times
    </button>
  );
}
```

With the `useState` hook we can create a state variable called `count` and a function called `setCount` to update that variable. We can then use that variable to display the count of how often the button was clicked using the `{}` syntax.

## Reacting to State Changes

We can use the `useEffect` hook to react to state changes. For example, we can use the `useEffect` hook to display a message when the button was clicked more than 5 times:

```jsx
function Button() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    if (count > 5) {
      alert('You clicked the button more than 5 times!');
    }
  }, [count]);

  return (
    <button onClick={() => setCount((c) => c + 1)}>
      I was clicked {count} times
    </button>
  );
}
```

The function inside the `useEffect` hook will be called every time the state variable `count` changes.

## Styling

Now we have a working button component. But it doesn't look very nice. Let's add some styling to make it look better.

### Using modules

We can use CSS to style our components. We can create a new file called `Button.module.css`. We can use this file to define the styles for our button component.

```css
.button {
  background-color: #000;
  color: #fff;
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
```

Now we can import the styles in our button component.

```jsx
import styles from './Button.module.css';

export default function Button() {
  return <button className={styles.button}>Click me</button>;
}
```

### Using the styles attribute

We can also use the `style` attribute to style our components.

```jsx
export default function Button() {
  return (
    <button
      style={{
        padding: '10px 20px',
        border: '1px solid #000',
        borderRadius: '5px',
      }}
    >
      Click me
    </button>
  );
}
```

### Using tailwindcss

We can also use a CSS framework like [tailwindcss](https://tailwindcss.com/) to style our components. We can use the `className` attribute to add tailwindcss classes to our components.

```jsx
export default function Button() {
  return (
    <button className="bg-cyan-800 text-white px-3 py-2 uppercase">
      Click me
    </button>
  );
}
```

## External packages

A lot of people have already created packages that we can use in our project. We can use the [npm](https://www.npmjs.com/) registry to find packages. Let's say we want to add icons in our project. We can use the [react-icons](https://www.npmjs.com/package/react-icons) package to add icons to our project.

```bash
npm install react-icons
```

Now we can import the icons we want to use in our project.

```tsx
import { FaUser } from 'react-icons/fa';

function Button() {
  return <button onClick={() => alert('I was clicked')}>Click me!</button>;
}

export default function App() {
  return (
    <div>
      <h1>Hello this is my App</h1>
      <p>
        And here is an icon: <FaUser />
      </p>
      <Button />
    </div>
  );
}
```
