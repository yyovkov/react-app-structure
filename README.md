# Intermediate Folder Structure

Original Document: [How To Structure React Projects From Beginner To Advanced](https://blog.webdevsimplified.com/2022-07/react-folder-structure/)

## Introduction

Already from the image above you will notice that this folder structure includes a ton more folders which cover pretty much any file type you can think of in a React project. For the most part with a folder structure like this you should have almost no files in the root of your `src` folder other than things like your `index.js` file.

The other big change between this folder structure and the simple folder structure is that we now are breaking our project into pages which encapsulate all the logic for specific pages into one single location. This is really useful on larger projects since now your can find all the information related to your pages in one folder instead of having to search across multiple folders and sift through unrelated files to find what you want.

You will also notice that our tests are now localized to the specific folder/files they are testing. This makes it easier to see which code is tested which in general just makes testing code easier when the tests are located in the same location as the code being tested.

## Structure

``` bash
├── assets
│   └── structure.png
├── components
│   ├── __tests__
│   ├── form
│   └── ui
├── context
├── data
├── hooks
├── pages
│   ├── Home
│   ├── Login
│   │   ├── LoginForm.js
│   │   ├── __tests__
│   │   ├── index.js
│   │   └── useLogin.js
│   ├── Settings
│   └── Signup
└── utils
```

## Folder Structure Description

### pages

The biggest change to this folder structure is the addition of the `pages` folder. This folder should contain one folder for each page in your application. Inside of those page specific folders should be a single root file that is your page (generally `index.js`) alongside all the files that are only applicable to that page. For example in the above image we have a `Login` page which contains the root file `index.js`, a component called `LoginForm`, and a custom hook called `useLogin`. This component and hook are only ever used in the `Login` page so they are stored with this page instead of being stored in the global `hooks` or `components` folders.

This separation of page specific code from your more general global code is the biggest benefit of this system over the simple folder structure. It is easier to see what your application is doing when all the relevant code is collocated in a single folder.

### components

Another big change you will notice with this example is that our `components` folder is further broken down into subfolders. These subfolders are really useful since they help keep your components organized into different sections instead of just being one massive blob of components. In our example we have a `ui` folder which contains all our UI components like buttons, modals, cards, etc. We also have a `form` folder for form specific controls like checkboxes, inputs, date pickers, etc.

You can customize and breakdown this `components` folder however you see fit based on your project needs, but ideally this folder shouldn’t get too large as many of your more complex components will be stored in the `pages` folder.

### hooks

The final folder that is a repeat from the simple folder structure is the `hooks` folder. This folder is pretty much identical to the previous `hooks` folder, but instead of storing every hook in your application it will only store the global hooks that are used across multiple pages. This is because all page specific hooks are stored in the `pages` folder.

### assets

The `assets` folder contains all images, css files, font files, etc. for your project. Pretty much anything that isn’t code related will be stored in this folder.

### context

The `context` folder stores all your React context files that are used across multiple pages. I find on larger projects you will have multiple context you use across your application and having a single folder to store them is really useful. If you are using a different global data store such as Redux you can replace this folder with a more appropriate set of folders for storing Redux files instead.

### data

The `data` folder is similar to the `assets` folder, but this is for storing our data assets such as JSON files that contain information used in our code (store items, theme information, etc). This folder can also store a file that contains global constant variables. This is useful when you have lots of constants you use across your application, such as environment variables.

### utils

The final new folder is the `utils` folder. This folder is for storing all utility functions such as formatters. This is a pretty straightforward folder and all the files in this folder should likewise be straightforward. I generally like to only store pure functions in this folder since if a utility function has side effects then it is most likely not just a simple utility function. Obviously there are exceptions to this rule, though. Also, if you are unfamiliar with pure functions check out [complete pure functions guide](https://blog.webdevsimplified.com/2020-09/pure-functions/).

## Pros and Cons

### Pros

The biggest benefit to this new system is that all your files have their own folder. The actual root `src` folder should have almost no files in it.

Another huge benefit is that your files are now collocated based on the page they are used in. This is good since generally as a project grows it is more and more important to have files that are used together stored together since it makes understanding, writing, and reading code easier as it reduces the amount of global code stored in your general `components`, `hooks`, etc. folders.

### Cons

The biggest con to this system is that as your application grows even larger your `pages` folder will start to become less and less useful. This is because as your application gets more pages it is more common that a single feature will be used across multiple pages instead of just one. When this happens you need to move the code out of the `pages` folder and into the other folders in your app which lessens the usefulness of your `pages` folder and bloats your other folders.

For example, if you have a simple todo list application that stores your todo list on just one page then the `pages` folder for your todo page can store all the code for your todos. If you then add a second page that lets your group todos under projects you now have two pages that need to show todo information so you can no longer keep these todo files in your `pages` folder. At a certain size nearly all your code will be shared across multiple pages which is where the advanced folder structure comes in.

## Folder Structure Implementation

* Create React Project

``` bash
mkdir project_name
cd project_name
npm create vite@latest . -- --template react
```

* Create directory structure

``` bash
mkdir src/{components,context,data,hooks,pages,utils}
mkdir src/components/{__tests__,form,ui}
mkdir src/pages/{Home,Login,Settings,Signup}
mkdir src/pages/{Home,Login,Settings,Signup}/__tests__
touch src/pages/{Home,Login,Settings,Signup}/index.js
touch src/Pages/Login/{LoginForm.js,useLogin.js}
```

* Start React project

``` bash
npm install
npm run dev
```
