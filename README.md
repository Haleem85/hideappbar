# [hideappbar](https://www.npmjs.com/package/hideappbar)

This repository is a [node](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiLxfOkxsT4AhVR6LsIHTqCDToQFnoECBMQAQ&url=https%3A%2F%2Fnodejs.org%2F&usg=AOvVaw1tY2p-vJFWJmxWlq4sTxCn) and got developed as practical activity for the tutorial entitled [How to build a React custom component library with Theme UI](https://blog.logrocket.com/build-react-custom-component-library-theme-ui/)

The package has been named hideappbar , this name was made randomly as I considered building this package for only self-learning try and it is a good idea to document its result in a public repository.

## Install hideappbar package

[hideappbar package link in npm](https://www.npmjs.com/package/hideappbar)

```js
npm i hideappbar
```

### HideAppBar use

Once installing finished go to your Bar component file import `HideAppBar`,`HideOnScroll`,`Button` and `Input` from `hideappbar` and insert them in your component.

```js

            import {HideAppBar, HideOnScroll, Button ,Input} from "hideappbar";

    const App =()=>{
    ...

return (

 <!-- To insert custom menu items in navbar -->

<HideOnScroll>

<!-- <{children elements}> -->

</HideOnScroll>

 <!-- to use default navbar  -->

 <HideAppBar />

 <!-- use input -->

<Input id="myInput" disabled ={false} label="submit" message="message text" error={true} success={true}
onChange="<{onChangeAction}>" placeholder="Type username"/>

<!-- use Button -->

<Button size="medium" primary={true} disabled={false} onClick="onClickAction"
/>
...
)

```

To get Tutorial text clicon:[How to build a React custom component library with Theme UI]("./Tutorial.md")]
