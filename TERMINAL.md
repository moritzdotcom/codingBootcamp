# The Terminal

The Terminal is the window to your computer. It is a text-based interface to the system. You can use it to navigate your file system, run programs, and execute a lot of other tasks. It is a very powerful tool and you will use it a lot as a developer.

## Navigation

### pwd

`pwd` stands for "print working directory". It shows you the path to the directory you are currently in.

### ls

`ls` lists the contents of the current directory. You can add the `-l` flag to get a long listing, which includes file permissions, ownership, size, and modification date.

### cd

`cd` stands for "change directory". You can use it to navigate to a different directory. You can use `cd ..` to go up one directory, and `cd ~` to go to your home directory.

## Working with files

### touch

`touch` creates a new file. You can use it like this: `touch index.html`.

### mkdir

`mkdir` creates a new directory. You can use it like this: `mkdir my-new-directory`.

### cp

`cp` copies a file. You can use it like this: `cp index.html index2.html`.

### mv

`mv` moves a file. You can use it like this: `mv index.html index2.html`. You can also use it to rename a file: `mv index.html index2.html`.

### rm

`rm` removes a file. You can use it like this: `rm index.html`.

### rmdir

`rmdir` removes a directory. You can use it like this: `rmdir my-directory`.

### cat

`cat` prints the contents of a file to the terminal. You can use it like this: `cat index.html`.

## Commands we will use frequently

### code

`code .` opens the current directory in VS Code.

### node

`node` runs a JavaScript file or starts a Node.js REPL where you can run JavaScript code. You can use it like this: `node index.js`.

### npm

`npm` is the Node Package Manager. It is used to install and manage packages. You can use it like this: `npm install react`.
We also use it to interact with our applications. For example, to start a Next.js application, we use `npm run dev`.

### git

`git` is a version control system. It is used to track changes in your code and collaborate with others. You can use it like this: `git add .` to add all files to the staging area, and `git commit -m "Add index.html"` to commit the changes to the repository. We will use the built in version control in VS Code, but it is good to know the basics of git.

### npx

`npx` is a tool that comes with npm. It is used to run packages without installing them. You can use it like this: `npx create-next-app@latest`.
