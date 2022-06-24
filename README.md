# [hideappbarr](https://www.npmjs.com/package/hideappbarr)

This repository is a [node](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwiLxfOkxsT4AhVR6LsIHTqCDToQFnoECBMQAQ&url=https%3A%2F%2Fnodejs.org%2F&usg=AOvVaw1tY2p-vJFWJmxWlq4sTxCn) and got developed as practical activity for the tutorial entitled [How to build a React custom component library with Theme UI](https://blog.logrocket.com/build-react-custom-component-library-theme-ui/)

The package has been named hideappbarr , this name was made randomly as I considered building this package for only self-learning try and it is a good idea to document its result in a public repository.

## Install hideappbarr package

[hideappbarr package link in npm](https://www.npmjs.com/package/hideappbarr)

```js
npm i hideappbarr
```

### HideAppBarr use

Once installing finished go to your Bar component file import `HideAppBarr`,`HideOnScroll`,`Button` and `Input` from `hideappbarr` and insert them in your component.

```js

import {HideAppBarr, HideOnScroll, Button ,Input} from "hideappbarr";

const App =()=>{
       ...

   return (

    <!-- To insert custom menu items in navbar -->

   <HideOnScroll>

   <!-- <{children elements}> -->

   </HideOnScroll>

    <!-- to use default navbar  -->

    <HideAppBarr />

    <!-- use input -->

   <Input id="myInput" disabled ={false} label="submit" message="message text" error={true} success={true}
   onChange="<{onChangeAction}>" placeholder="Type username"/>

   <!-- use Button -->

   <Button size="medium" primary={true} disabled={false} onClick="onClickAction"
   />
   ...
   )
};
```

To get Tutorial text clicon:[How to build a React custom component library with Theme UI]("./Tutorial.md")]
