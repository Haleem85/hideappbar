# [How to build a React custom component library with Theme UI](https://blog.logrocket.com/build-react-custom-component-library-theme-ui/)

===========================================================


React is a JavaScript toolkit that facilitates the creation of beautiful user interfaces for both online and mobile apps. It easily interfaces with other JavaScript frameworks and libraries and has short, reusable components.

Because of their great modularity, React component libraries speed up UI development and also provide a lot of freedom. There are several [popular React UI libraries](https://blog.logrocket.com/top-9-ui-libraries-kits-react/); however, they may not offer the level of customization needed for all projects.

In this tutorial, we’ll review how to build and publish a custom component library in React with [Theme UI](https://theme-ui.com) using TypeScript.

## What is Theme UI?

Theme UI is a library that uses constraint-based design concepts to create themeable user interfaces. With a broad API for best-in-class developer ergonomics, Theme UI can be used to create bespoke component libraries, design systems, web applications, Gatsby themes, and more.

## Getting started

This hands-on tutorial has the following prerequisites:

-   [Node.js](https://nodejs.org/) installed
-   Ubuntu 20.04, or the OS of your choice
-   VS Code, or any IDE of your choice

## Project setup

We’ll start by running the following command to create a folder for our project:

mkdir themecomponentui && cd themecomponentui

Next, we’ll initialize a new React project using the `npm init` command to create a `package.json` file. Then, we’ll install React and TypeScript with the following command:

npm i \-D react @types/react typescript

The `-D` flag in the above command denotes that the modules should be installed as `devDependencies` because we’ll need them during our build process.

With React and TypeScript installed, let’s organize our project according to the below folder structure:

![📦](https://s.w.org/images/core/emoji/14.0.0/svg/1f4e6.svg)themecomponentui  
┣ ![📂](https://s.w.org/images/core/emoji/14.0.0/svg/1f4c2.svg)src  
┃ ┣ ![📂](https://s.w.org/images/core/emoji/14.0.0/svg/1f4c2.svg)components  
┃ ┃ ┣ ![📂](https://s.w.org/images/core/emoji/14.0.0/svg/1f4c2.svg)Button  
┃ ┃ ┣ ![📂](https://s.w.org/images/core/emoji/14.0.0/svg/1f4c2.svg)Input

We made a custom demo for .  
No really. Click here to check it out.

---

Click here to see the full demo with network requests

.inline-demo {width: 100%; max-width:700px;display:none;margin-bottom: 2rem;transition: filter 0.5s ease;padding: 1.5rem;border-radius: 5px;filter: drop-shadow(5px 0px 15px #afafaf); background: linear-gradient(-45deg, #764abc, #7a49a5, #4974a5,#4A4A4A); background-size: 400% 400%; animation: gradient 10s ease infinite;} .inline-demo:hover{filter:drop-shadow(1px 0px 5px #d7d7d7) !important;}@keyframes gradient { 0% { background-position: 0% 50%; } 50% { background-position: 100% 50%; } 100% { background-position: 0% 50%; } }#blog-personalized-demo-link:hover{text-decoration:none;} .personalize-button {background: #4ABC76; width: 35%; border-radius: 25px; text-decoration: none; color: #fff; line-height: 18px; display: block; margin: 20px auto 5px auto; border:0px; padding: 20px; letter-spacing: 0.1px; box-shadow: 0px 0px 50px 10px rgba(0,0,0,0.3); transition: all 0.25s linear;} .personalize-button:hover{ color: #4ABC76; background: #fff !important; cursor:pointer; }@media all and (max-width: 600px){.personalize-button{width: 80%;}}

Now, let’s configure TypeScript for our project.

## Configuring TypeScript

We’ll use TypeScript to build the components that will enable us to use the library as a module.

First, we’ll configure TypeScript by creating a `tsconfig.json` file using the following command:

npx tsc \--init

Then, we’ll update the `tsconfig.json` file with the following snippet:

{
"compilerOptions": {
"esModuleInterop": true,
"strict": true,
"skipLibCheck": true,
"jsx": "react",
"module": "ESNext",
"declaration": true,
"declarationDir": "types",
"sourceMap": true,
"outDir": "dist",
"moduleResolution": "node",
"emitDeclarationOnly": true,
"allowSyntheticDefaultImports": true,
"forceConsistentCasingInFileNames": true,
},
"exclude": \[
"dist",
"node_modules",
\],
}

In the above code, we added the following configurations:

-   `"jsx": "react"`: Transforms JSX code into React code
-   `"skipLibCheck": true`: Skips type checking the declaration files
-   `"module": "ESNext"`: Generates Modern JavaScript modules for our library (ES6 or higher)
-   `"declarationDir": "types"`: Sets up a directory for the .d.ts files
-   `"sourceMap": true`: Enables mapping of JavaScript code back to its TypeScript file origins for debugging
-   `"outDir": "dist"`: Sets up the directory for project build
-   `"moduleResolution": "node"`: Follows Node.js rules for finding modules
-   `"emitDeclarationOnly": true`: Allows Rollup to generate JavaScript export type declarations

Now that TypeScript is configured, let’s move on to configuring Rollup.

## Configuring Rollup

[Rollup](https://www.npmjs.com/package/rollup) is a JavaScript module bundler that combines tiny chunks of code to create something larger and more sophisticated, like a library or application. Instead of using unique solutions like CommonJS and AMD, it leverages the standardized ES module structure for code.

To get started with Rollup, we’ll install it using the following command:

npm i \-D rollup

In the above code, we added the `-D` flag to the Rollup installation command to add it to our `devDependencies`. Once the installation is completed, we’ll also install the following Rollup plugins:

-   [@rollup/plugin-node-resolve](https://www.npmjs.com/package/@rollup/plugin-node-resolve): To resolve third-party modules in `node_modules`
-   [@rollup/plugin-typescript](https://www.npmjs.com/package/@rollup/plugin-typescript): For seamless Rollup and TypeScript integration
-   [@rollup/plugin-commonjs](https://www.npmjs.com/package/@rollup/plugin-commonjs) : To convert CommonJS modules to ES6 modules
-   [@rollup-plugin-dts](https://www.npmjs.com/package/rollup-plugin-dts): To rollup our `.d.ts` files
-   [@types/rollup-plugin-peer-deps-external](https://www.npmjs.com/package/@types/rollup-plugin-peer-deps-external) : To automatically externalize `peerDependencies` in a rollup bundle
-   [@rollup-plugin-terser](https://www.npmjs.com/package/rollup-plugin-terser): To minify the generated ES bundle

We’ll run the following command to install the plugins:

npm i \-D @rollup/plugin\-node\-resolve @rollup/plugin\-commonjs @rollup/plugin\-typescript rollup\-plugin\-peer\-deps\-external rollup\-plugin\-terser rollup\-plugin\-dts

When the installation is complete, we’ll configure Rollup by creating a `rollup.config.js` file in the project root directory using the following snippets:

import resolve from "@rollup/plugin-node-resolve";
import commonjs from "@rollup/plugin-commonjs";
import typescript from "@rollup/plugin-typescript";
import dts from "rollup-plugin-dts";
import { terser } from "rollup-plugin-terser";
import peerDepsExternal from 'rollup-plugin-peer-deps-external';
const packageJson \= require("./package.json");

export default \[
{
input: "src/index.ts",
output: \[
{
file: packageJson.main,
format: "cjs",
sourcemap: true,
},
{
file: packageJson.module,
format: "esm",
sourcemap: true,
},
\],
plugins: \[
peerDepsExternal(),
resolve(),
commonjs(),
typescript({ tsconfig: "./tsconfig.json" }),
terser(),
\],
external: \["react", "react-dom"\]
},
{
input: "dist/esm/types/index.d.ts",
output: \[{ file: "dist/index.d.ts", format: "esm" }\],
plugins: \[dts()\],
},
\];

In the above code, we configured CommonJS and ES modules to handle the project build process. This will enable us to use named export and tree shaking. It also provides enhanced static analysis, browser support, and compatibility with other JavaScript versions.

Next, we need to specify the path to the CommonJS files and ES modules in the `package.json` file. We’ll open the `package.json` file and add the following snippet configurations:

"main": "dist/cjs/index.js",
"module": "dist/esm/index.js",

Finally, we’ll add the build command inside the `scripts` object:

...
"scripts": {
...
"build": "rollup -c"
},
...

## Creating custom components

Now, let’s create our custom components. First, we’ll install Theme UI:

npm install \-D theme\-ui @emotion/react @emotion/styled @mdx\-js/react

Theme UI is a flexible API framework, so we can choose to use a library of primitive UI components or use the [`sx` prop](https://theme-ui.com/sx-prop/). For the demonstration purpose of this tutorial, we’ll use the `sx` prop.

## Creating the button component

Next, let’s create the button component. We’ll create `Button.tsx` and `index.ts` files in the `src/components/Button` folder.

Open the `Button.tsx` file and add the following snippets:

/\*\* @jsxImportSource theme-ui \*/
import \* as React from "react";
import { MouseEventHandler } from "react";

export interface ButtonProps {
label?: string;
color?: string;
fontFamily?: string
onClick?: MouseEventHandler<HTMLButtonElement\>
}

const Button \= (props: ButtonProps) \=> {
return <button onClick\={props.onClick} sx\={{ color: props.color, fontFamily: props.fontFamily }}>{props.label}</button\>;
};
export default Button;

In the above code, we added the `/** @jsxImportSource theme-ui */` comment to the top of the file to enable the Theme UI `sx` props.

Next, we imported the React framework `MouseEventHandler` method to enable button click events.

Then, we defined the `interface` `ButtonProps`, specifying the `Button` component properties. The `?` symbol denotes an optional property (e.g., `color?: string`), meaning TypeScript will not throw an error if we do not provide that property in the component.

Next, we created the `Button` component and set the styling using Theme UI’s `sx` props with other properties.

Now, let’s export the `Button` component in the `index.ts` file using the following snippet:

export { default } from './Button'

## Creating the `Input` component

We’ll create the `Input` component by creating `Input.tsx` and `index.ts` files in the `src/components/Input` folder.

Open the `Input.tsx` file, and add the following snippet:

/\*\* @jsxImportSource theme-ui \*/
import \* as React from "react";
import { ChangeEventHandler } from "react"

export interface InputProps {
label?: string;
disabled?: boolean;
fontFamily?: string;
placeholder?: string;
paddding?: string;
id?: string;
onChange?: ChangeEventHandler<HTMLInputElement\>
}

const Input \= (props: InputProps) \=> {
return (
<div\>
<label htmlFor\={props.id ? props.id : 'text'}>{props.label}</label\>
<input type\='text' id\={props.id ? props.id : 'text'} disabled\={props.disabled} placeholder\={props.placeholder} sx\={{ padding: !props.paddding && "4px", display: 'block' }}></input\>;
</div\>
);
};
export default Input;

In the above code, we added the `/** @jsxImportSource theme-ui */` comment at the start of the file to use the Theme UI’s `sx` prop to style the component.

Next, we defined the `Input` component’s `interface`. The `onChange?` property will enable us to add an `onChange` event to the input.

We created the `Input` component, which takes in `props` that match the `InputProps` interface, and styled the component using Theme UI’s `sx` prop and other properties.

Now, let’s export the `Input` component in the `index.ts` file using the following command:

export { default } from './Input'

We’ll create an `index.ts` file in the `src/components` folder, and export the components like so:

export { default as Button } from './Button';
export { default as Input } from './Input'

Now, we’ll build the project:

npm run build

The above command will create a `dist` folder in the project root directory.

## Publishing to npm

The next step is to publish our newly created components to npm so that we can use them in our project and share them with friends.

To get started, log into your npm account:

npm login

If you don’t have an account, you can [sign up for an npm account here](https://www.npmjs.com).

After logging in, enter your account credentials to get authenticated. An OTP code will be sent to your registered email address. Enter the OTP pin when requested.

Now, publish your package by running the following command:

npm publish \--access public

You’ve successfully published a React custom component library to npm!

## Conclusion

In this tutorial, we introduced the Theme UI library and demonstrated how to use Theme UI to build a custom React component library. We also demonstrated how to configure TypeScript and Rollup for the project build and how to publish a custom library to npm. You can extend this tutorial by creating more components with Theme UI, such as forms, boxes, and grids.

Thanks for reading. Please feel free to share and comment below.

## Links

-   [How to build a React custom component library with Theme UI](https://blog.logrocket.com/build-react-custom-component-library-theme-ui/)

-   [Build a component library with React and TypeScript](https://blog.logrocket.com/build-component-library-react-typescript/)
