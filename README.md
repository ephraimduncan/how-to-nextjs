# How To Next.js

_A guide to Vercel's Hybrid Framework for React Applications_

## Introduction

If you've been paying attention to the web development world, you've probably heard a lot about Next.js. Today I'm going to tell you all I know about Next.js,probably not all of them but something to base your journey into Next.js on.

Next.js is an opinionated open-source web development framework built on top of Node.js that enables server-side rendering and the generation of static websites in React-based web applications. React is a JavaScript library used to create web applications that are rendered in the client's browser using JavaScript.

Next.js was created by Vercel and allows you to create client-side and server-side applications. The framework has a zero-config approach and allows you to write scalable, performant React applications. Next.js provides with a variety of opinionated features out of the box, including:

- Routing using Next's built-in router making use of React Hooks.
- Image Optimization using Next's `Image` component built upon html `img` tags.
- Fast Refresh to update the page without reloading.
- Hosting of Static Files and Assests in a `public` folder.
- Built-in CSS/Sass Support.
- API Routes for easier API management. For any file added to the pages/api directory is treated as an API endpoint with a corresponding API route that can be used for backend functionality and can also be used to run serverless functions.
- Internationalization Routing
- File-System Based Routing. Organizing files and subdirectories within a `pages` directory automatically results in corresponding routes.
- TypeScript Support
- Code Splitting and Bundling to load code on demand.
- Server Side Rendering to render the page on the server.

In this tutorial, we’ll learn the basics of Next.js and at the end of the tutorial, we will create a Simpe Image Gallery. In the process, you’ll see how simple it can be to create a web application powered by Next.js and hosted on Vercel.

Our simple Next.js web app has:

- An input page that allows users to search for a keyword and display images based on the keyword provided.
- A preview page to view a full detailed image of an images clicked by the user.
- A gallery page that displays all of the images fetched from an external API.
- An API Route to fetch data from an external API and send it to the Next.js app.

For this tutorial, you should already be familiar with JavaScript. It’s okay if you’re not familiar with Next.js as the tutorial begins with an introduction to the framework.

## Installation and Setup

The `create-next-app` CLI tool is the simplest way to create a new Next.js application. It can be installed using npm. You can create a new Next.js application using the following command:

```sh
npx create-next-app my-next-app
```

Once the installation is finished, you can navigate to the directory where the application was created and open it in your prefered code editor. The default project structure is as follows:

    my-next-app
    ├── pages
    ├── public
    ├── pages
    │   ├── api
    │   │   └── hello.js
    │   ├── _app.js
    │   └── index.js
    ├── styles
    │   ├── global.css
    │   └── Home.module.css
    ├── .env.local
    ├── .eslintrc.json
    ├── .gitignore
    ├── README.md
    ├── next.config.js
    ├── package.json
    └── yarn.lock

Once everything is in place, you can start the application by opening the terminal and navigating to the directory where the application was created in the terminal. You can then run the following command to start your application.

```sh
yarn dev

# or

npm run dev
```

We are running our application in the development server. This means that the application will be served from the localhost:3000 port locally on our machine. To preview the application running, you can open a browser and navigate to http://localhost:3000.

We should get a preview of the application like this:

![Next.js Preview](./static/localhost.png)

If everything is setup correctly, you should see the page on the browser without any issues. Next, we locate the `index.js` file in the `pages` directory. This file is the entry point for the application. We are going to replace all the context of the `index.js` with a simple react component.

```jsx
export default function HomePage() {
  return <div>Thank u, next</div>;
}
```

This is how simple Next.js works. Whenever you put a JavaScript file in the `pages` directory, it is automatically a route, no configuration needed (so a `about.js` will become `localhost:3000/about`). Along with this, you can include dynamic routes (as in, ones with variable names, and do shallow routing (meaning you can change the URL without calling data fetching methods again).

![Next.js Preview](./static/localhost-2.png)

Your new change once saved should reflect in the browser automatically using React Fast Refresh. No need to refresh the page and no configuration is needed. It all works out of the box!

## Navigation Between Pages

In Next.js, a page is a React Component exported from a file in the pages directory. The Next.js app we built so far only has one page. Many different pages can be found on most websites and web apps. Let's look at how we can expand our app with more pages. It's simple to create a new page. Just create a file in the `pages` directory to get a route based on the file name.

Lets begin by replacing our `pages/index.js` file with the following:

```jsx
export default function HomePage() {
  return <h1>Home Page</h1>;
}
```

In the `pages` directory, create two new files called `about.js` and `contact.js`. Add the following to the files respectively:

```jsx
// about.js
export default function AboutPage() {
  return <h1>About Page</h1>;
}
```

```jsx
// contact.js
export default function ContactPage() {
  return <h1>Contact Page</h1>;
}
```

In the browser, go to either the `/about` or `/contact` route. The pages should display without issue. The next thing is to navigate between the pages on the browser.
The `<a>` HTML element is used to link between pages on a website. In Next.js, you use the Link Component from `next/link` to wrap the `<a>` tag. `Link` enables client-side navigation to another page inside the application. Unlike the native `<a>` element, the `Link` component does not refresh the page when the page is navigated, allowing client-side navigation between two pages in the same Next.js project.

To start navigation, let's first import the `Link` component. At the top of your `pages/index.js` route, import the `Link` with the following:

```js
import Link from "next/link";
```

Then replace the content of the `HomePage` component with the following:

```jsx
export default function HomePage() {
  return (
    <div>
      <h1>Home Page</h1>
      <div>
        <Link href="/about">
          <a>About</a>
        </Link>
      </div>
      <div>
        <Link href="/contact">
          <a>Contact</a>
        </Link>
      </div>
    </div>
  );
}
```

Now let's add a `Link` component on the `about.js` and `contact.js` pages to link back to the home component. Import it first then replace the `<h1>` in both pages with the following respectively:

```jsx
// about.js
export default function AboutPage() {
  return (
    <div>
      <h1>About Page</h1>
      <Link href="/">
        <a>Home</a>
      </Link>
    </div>
  );
}
```

```jsx
// contact.js
export default function ContactPage() {
  return (
    <div>
      <h1>Contact Page</h1>
      <Link href="/">
        <a>Home</a>
      </Link>
    </div>
  );
}
```

How the `Link` component works is that it wraps around the `<a>` tag and adds a `href` attribute to it. The `href` attribute is the URL or the page route that the link will navigate to. In the `/about` and `/contact` pages, the `href` attribute on the `Link` component is set to `/`. The router will automatically route files named `index` to the root of the directory. `pages/index.js` will be associated with the `/` route.

We can now preview the `index.js` page in the browser and see the `Link` component working in action.

![Next.js Navigation](./static/next-navigation.gif)

## Styling, Assets and Metadata

### Assets

Next.js has support for static public folders and serves all static site images, CSS, Google Site Verification,robots.txt, and favicon.ico. In the root directory with the public folder, you access everything in production or built time.

Let's test it out by rendering a static image on a page. In the `pages` directory, create a new `pages/image.js` page. We are simply going to render a static image stored in the public folder on the page.

In the public folder, add a new image file and mind the name of the image and file extension. In the `image.js` file, let's add the following:

```js
export default function ImagePage() {
  return (
    <div>
      <h1>Next.js Logo</h1>
      <img src="/logo.png" alt="Logo" width={128} height={128} />;
    </div>
  );
}
```

![Next.js Navigation](./static/next-image.png)

The page should render as above.

If everything is set up correctly, the image should display correctly in the browser. You notice that the image's `src` is not a relative path, but rather a route. This is a unique Next.js feature. The static images route-path allows the same image to be referenced in the `<img> `tag code on several pages utilizing the root URL. For example, `src=/logo.png`.

### Metadata

There is a `Head` component with Next.js that can be imported from `next/head`. This `Head` component is basically a built-in component that Next.js provides to append elements, such as title and meta tags, to the `<head>` element to improve SEO. The advantage of this component is that, it is on a per page basis, and not a global level meaning each page can have specific SEO information related to that page!

Let's improve the `pages/index.js` file with the `Head` component. Import the `Head` component first:

```js
import Head from "next/head";
```

Let's improve the HomePage component:

```js
export default function HomePage() {
  return (
    <div>
      <Head>
        <title>Home</title>
        <meta name="description" content="Next.js is a React Framework" />
      </Head>
      ...
    </div>
  );
}
```

Try accessing http://localhost:3000/. The browser tab should now say “Home”. By using your browser’s developer tools, you should see that the title and meta tags were added to <head>. You can go ahead and add the `Head` component to the `about.js` and `contact.js` pages as well.

### Styling

Next.js offers many ways to support CSS in your application. Whether you prefer utility CSS with its classes or prefer CSS-in-JS, Next.js has you covered. We are going to implement two styling options. Global CSS for the whole application and component-specific styling.

We want to style the `<h1>` tags in the pages but first let's make into a resuable React component and use it across different pages. In the root directory, create a `components` directory. Create a new `components/Header.js` file and add the following:

```jsx
export default function Header({ title }) {
  return <h1>{title}</h1>;
}
```

We can refactor the `pages/index.js` file to use the `Header` component. Import the `Header` component first:

```jsx
import Header from "../components/Header.js";
```

In the `pages/index.js` file, replace the `<h1>` with the following:

```jsx
<Header title="Home Page" />
```

We can save our file and the component will render correctly. Now that we have abstracted the `<h1>` tag, we can use it in the `about.js` and `contact.js` pages as well. Let's focus on styling the component. Next.js support CSS Modules out of the box.

CSS modules allow you to isolate your CSS by creating files for style-specific components. They are very easy to use, as they are simple CSS but have `.module.css` as the extension.

In the `components` directory, add a new `Header.module.css` file and add the following:

```css
.title {
  color: red;
}
```

In the Header components file, we can import the style as:

```jsx
import styles from "./Header.module.css";
```

Replace the `<h1>` tag with the following:

```jsx
<h1 className={styles.title}>{title}</h1>
```

We are using the styles from the `Header.module.css` file as a class on the `<h1>` tag. We can see the styling in action on the browser.

Next, we are Implement global styling for our application. The styles created in `global.css` will then apply to your entire application. To implement global styling, we add the styles to a `global.css` file in the `styles` directory and import it in the `_app.js` file as the App component initializes all the pages in your Next.js pages.

Let's change the background color of the application. In your `styles/global.css`, add the following:

```css
html {
  background-color: #63cad6;
}
```

In the `_app.js` file, import the stylesheets from the `styles` directory as follows:

```js
import "../styles/globals.css";
```

We can also navigate between the pages to see that the style is affecting the whole application snd view the changes from browser. Everything is working 🎉. You can take a break now, you have come a really long way.
