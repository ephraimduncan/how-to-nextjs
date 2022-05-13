# How To Next.js

_A guide to Vercel's Hybrid Framework for React Applications_

## Introduction

If you've been paying attention to the web development world, you've probably heard a lot about Next.js. Today I'm going to tell you all I know about Next.js,probably not all of them but something to base your journey into Next.js on.

Next.js is an opinionated open-source web development framework built on top of Node.js enabling React based web applications functionalities such as server-side rendering and generating static websites. React is a JavaScript library that is traditionally used to build web applications rendered in the client's browser with JavaScript.

Created by Vercel, Next.js is capable of creating applications that run both on the client and the server. The framework allows you to build scalable, performant React code and comes with a zero-config approach. Next.js comes out of the box with a lot of opinionated features which include:

- Routing using Next's built-in router making use of React Hooks.
- Image Optimization using Next's `Image` component built upon html `img` tags.
- Fast Refresh to update the page without reloading.
- Host Static Files and Assests in a `public` folder.
- Built-in CSS/Sass Support
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
