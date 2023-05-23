# Next.JS

Now that we learned all the fundamentals, we can completely forget everything we learned so far and start learning Next.js. Just kidding! Or am I? Next.js is a Javascript framework. It is built on top of React and adds some features that make it easier to build web applications. Next.js is just a high-level layer that handles some of the more tedious tasks for us. It is still important to understand what is going on under the hood.

## Getting started

Let's create our first application:

```bash
npx create-next-app@latest

# Need to install the following packages:
#   create-next-app@latest
# Ok to proceed? (y) y

# ✔ What is your project named? sebi-bootcamp-app
# ✔ Would you like to use TypeScript with this project? Yes
# ✔ Would you like to use ESLint with this project? No
# ✔ Would you like to use Tailwind CSS with this project? Yes
# ✔ Would you like to use `src/` directory with this project? No
# ✔ Use App Router (recommended)? No
# ✔ Would you like to customize the default import alias? No

# Creating a new Next.js app in /Users/moritz/code/webdev/sebiBootcamp/sebi-bootcamp-app.

cd sebi-bootcamp-app

npm run dev
```

Now visit `http://localhost:3000` in your browser.

## Project structure

To understand how the project is structured, we can stop the development server with `ctrl + c` and open the project in VS Code with the `code .` command.

We see multiple files and folders. The most important are:

- **Pages**: Here we define the pages of our application. Each file in this folder will be a page. The file name will be the URL of the page. For example, `index.js` will be the home page, and `about.js` will be the about page (http://localhost:3000/about).
- **Public**: Here we put static files like images, fonts, etc.
- **Styles**: Here we put our CSS files.

## Pages

Here we can see the page we just saw in the browser (index.tsx). We can modify the page to get a cooler landing page like this:

```tsx
export default function Home() {
  return (
    <main>
      <h1>Welcome to Sebi Bootcamp!</h1>

      <p>
        Learn how to <code>code</code> in minutes!
      </p>

      <a href="/signup">Sign up</a>
    </main>
  );
}
```

Now we have a very cool landing page and a call to action to sign up. Lets build the signup page. We can do this by creating a new file called `signup.tsx` in the `pages` folder.

```tsx
export default function Signup() {
  return (
    <main>
      <h1>Sign up</h1>

      <form>
        <div>
          <label htmlFor="email">Email</label>
          <input type="email" id="email" />
        </div>

        <div>
          <label htmlFor="password">Password</label>
          <input type="password" id="password" />
        </div>

        <button type="submit">Sign up</button>
      </form>
    </main>
  );
}
```

## State

Lets bring the signup form to life by adding some state. As we learned in the `React` section, we can do this by using the `useState` hook.

```tsx
import { useState } from 'react';

export default function Signup() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  return (
    <main>
      <h1>Sign up</h1>

      <form>
        <div>
          <label htmlFor="email">Email</label>
          <input
            type="email"
            id="email"
            value={email}
            onChange={(e) => setEmail(e.target.value)}
          />
        </div>

        <div>
          <label htmlFor="password">Password</label>
          <input
            type="password"
            id="password"
            value={password}
            onChange={(e) => setPassword(e.target.value)}
          />
        </div>

        <button type="submit">Sign up</button>
      </form>
    </main>
  );
}
```

## Components

We can extract the form into a separate component to make the code more readable. We create a folder called `components` and create two files: `Input.tsx` and `Button.tsx`.

```tsx
// components/Input.tsx
interface InputProps {
  label: string;
  type: string;
  value: string;
  onChange: (e: React.ChangeEvent<HTMLInputElement>) => void;
}

export default function Input({ label, type, value, onChange }: InputProps) {
  return (
    <div>
      <label htmlFor={label}>{label}</label>
      <input type={type} id={label} value={value} onChange={onChange} />
    </div>
  );
}
```

```tsx
// components/Button.tsx
interface ButtonProps {
  onClick?: () => void;
  children: React.ReactNode;
}

export default function Button({ onClick, children }: ButtonProps) {
  return <button onClick={onClick}>{children}</button>;
}
```

## Fetching data & API routes

Now when we click on Sign up, we want to send the data to the server to create the User. We can do this by adding an `onSubmit` handler to the form.

```tsx
import { useState } from 'react';
import Input from '../components/Input';
import Button from '../components/Button';

export default function Signup() {
  const [email, setEmail] = useState('');
  const [password, setPassword] = useState('');

  const handleSubmit = async (e) => {
    e.preventDefault();

    const response = await fetch('/api/signup', {
      method: 'POST',
      body: JSON.stringify({ email: email, password: password }),
    });

    const data = await response.json();

    console.log(data);
  };

  return (
    <main>
      <h1>Sign up</h1>

      <form onSubmit={handleSubmit}>
        <Input
          label="email"
          type="email"
          value={email}
          onChange={(e) => setEmail(e.target.value)}
        />
        <Input
          label="password"
          type="password"
          value={password}
          onChange={(e) => setPassword(e.target.value)}
        />
        <Button type="submit">Sign up</Button>
      </form>
    </main>
  );
}
```

Lets create the API route that we are calling in the `handleSubmit` function. We can do this by creating a new file called `signup.ts` in the `pages/api` folder.

```ts
export default function signup(req, res) {
  const { email, password } = req.body;

  // We can store the user in the database, send a confirmation email, etc.
  // For now, we just return a success message.

  return res.status(200).json({ message: 'User created!' });
}
```
