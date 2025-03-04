# 04 Images

Let's add some images and how it works with Nextjs.

We will start from `03-styles`.

# Steps to build it

- `npm install` to install previous sample packages:

```bash
npm install
```

- Now, we want to add the `public/home-logo.png`:

_./src/components/app.layout.tsx_

```diff
...

export const AppLayout: React.FunctionComponent = (props) => {
  const { children } = props;

  return (
    <>
      <AppBar position="fixed">
        <Toolbar className={classes.toolbar} variant="dense">
+         <img src="/home-logo.png" />
          <Typography variant="h6" color="inherit">
            Rent a car
          </Typography>
...
```

- Issues related with approach:

  - The size needed for the design.
  - We don't need larger image sizes for smartphones or tables, only for desktop.
  - Render images is slow for initial page load.

- Let's use `next/image`:

_./src/components/app.layout.tsx_

```diff
import React from 'react';
+ import Image from 'next/image';
import AppBar from '@material-ui/core/AppBar';
...

export const AppLayout: React.FunctionComponent = (props) => {
  const { children } = props;

  return (
    <>
      <AppBar position="fixed">
        <Toolbar className={classes.toolbar} variant="dense">
-         <img src="/home-logo.png" />
+         <Image src="/home-logo.png" layout="fill" objectFit="contain"  />
          <Typography variant="h6" color="inherit">
            Rent a car
          </Typography>
...
```

> [Image docs](https://nextjs.org/docs/api-reference/next/image) > [Image examples github](https://github.com/vercel/next.js/tree/canary/examples/image-component/pages)
> It adapts image to the design
> Size `214kB` vs `44.5kB`
> First load the page and then the image.
>
> Blur effect supported since Next v11.
> [Nextjs Issue not supported](https://github.com/vercel/next.js/issues/18858) > [plaiceholder](https://github.com/joe-bell/plaiceholder) and [example with Nextjs](https://github.com/joe-bell/plaiceholder/tree/main/examples/next) > [Vanilla Blur Example](https://codepen.io/darajava/pen/GRZzpbB?editors=0110)

- Let's try `blur` effect:

_./src/components/app.layout.tsx_

```diff
import React from 'react';
import Image from 'next/image';
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';
+ import logo from '../../public/home-logo.png'
import * as classes from './app.layout.styles';

...

  return (
    <>
      <AppBar position="fixed">
        <Toolbar className={classes.toolbar} variant="dense">
-         <Image src="/home-logo.png" layout="fill" objectFit="contain" />
+         <Image src={logo} layout="fill" objectFit="contain" placeholder="blur" />
...

```

- Let's move this image inside a button:

_./src/components/app.layout.tsx_

```diff
import React from 'react';
import Image from 'next/image';
import AppBar from '@material-ui/core/AppBar';
import Toolbar from '@material-ui/core/Toolbar';
import Typography from '@material-ui/core/Typography';
+ import IconButton from '@material-ui/core/IconButton';
import logo from '../../public/home-logo.png'
import * as classes from './app.layout.styles';
...

export const AppLayout: React.FunctionComponent = (props) => {
  const { children } = props;

  return (
    <>
      <AppBar position="fixed">
        <Toolbar className={classes.toolbar} variant="dense">
+         <IconButton>
            <Image src={logo} layout="fill" objectFit="contain" placeholder="blur" />
+         </IconButton>
...

```

- Add some styles:

_./src/components/app.layout.styles.tsx_

```diff
import { css } from '@emotion/css';

export const toolbar = css`
  display: flex;
  flex-direction: row;
  column-gap: 1rem;
  row-gap: 1rem;
`;

+ export const iconButton = css`
+   width: 3rem;
+   height: 3rem;
+ `;
...

```

_./src/components/app.layout.tsx_

```diff
...
-         <IconButton>
+         <IconButton className={classes.iconButton}>
            <Image src={logo} layout="fill" objectFit="contain" placeholder="blur" />
          </IconButton>
```

# About Basefactor + Lemoncode

We are an innovating team of Javascript experts, passionate about turning your ideas into robust products.

[Basefactor, consultancy by Lemoncode](http://www.basefactor.com) provides consultancy and coaching services.

[Lemoncode](http://lemoncode.net/services/en/#en-home) provides training services.

For the LATAM/Spanish audience we are running an Online Front End Master degree, more info: http://lemoncode.net/master-frontend
