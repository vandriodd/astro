# Astro Basics 🪐

This README ccontains theoretical notes and key concepts to understand Astro.

> [!WARNING]
> Maybe some of the concepts are not 100% accurate because I'm just starting to learn Astro. If you find any mistakes, please let me know!

## Table of Contents

- [What is Astro?](#what-is-astro)

## Island Architecture 🏝

**Island Architecture** is a frontend design pattern where static pages contain "islands" of interactivity. These islands are reactive components that load JavaScript only when necessary, enhancing performance by reducing the amount of JavaScript loaded by default.

### Why Does It Matter?

- **Performance**: by not loading JavaScript on the client by default, pages load faster, improving user experience.
- **SEO**: static content is easily indexable by search engines, ensuring better SEO performance.
- **Framework Agnostic**: Astro allows you to use multiple UI libraries like React, Vue, Svelte, or Angular in the same project, providing flexibility in choosing the best rools for you needs.

> [!NOTE]
> Be sure to install the Astro VSCode extension, as Astro uses its own syntax, which is similar to JSX, but it's not the same.

## Astro Syntax ✍🏻

Astro files typically include the following sections:

### Script Block (`---`)

The section between the `---` is where you can write JavaScript, including imports, data fetching, and defining props.

```astro
---
import SomeComponent from '../components/SomeComponent.astro'
const data = await fetch('https://api.example.com/data');
---
```

### Template Block

Below the script block is the template section, which defines the rendered content. This may look like a React component, but it's not.

```astro
<SomeComponent data={data} />
```

### Style Block

At the bottom of the file, you can include styles within a `<style>` tag.

```astro
<style>
  h1 {
    color: blue;
  }
</style>
```

**Scoped styles**: styles in Astro are scoped to the specific component, similar to Vue or Svelte. This means they only apply to the elements withing the component where they are defined.

## Layouts and Components 🧩

- **Layouts**: Astro allows you to create reusable layouts that can be applied across different pages.
- **Components**: Astro minimizes boilerplate, enabling you to write less code while achieving the same functionality. Unlike other frameworks, you won't see and explicit "export" in components.

When you navigate to a page in your Astro project, the file served is typically `index.astro` located in the `/pages` directory.

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```plaintext
/
├── public/
│ └── favicon.svg
├── src/
│ ├── components/
│ │ └── Card.astro
│ ├── layouts/
│ │ └── Layout.astro
│ └── pages/
│ └── index.astro
└── package.json
```

Astro looks for .astro or .md files in the src/pages/ directory. Each page is exposed as a route based on its file name.

There's nothing special about src/components/, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the public/ directory.

## Available Commands 🛠️

Here are the key commands you can run with pnpm:

- `pnpm run dev`: Starts the Astro development server (`astro dev`).
- `pnpm run build`: Builds the project for production (`astro build`).
- `pnpm run preview`: Previews the built project (`astro preview`).
- `pnpm run astro`: Executes generic Astro commands.

> [!NOTE]
> Fun fact! Astro uses port 4321 for its dev server, like a countdown to a rocket launch!

## Fast Refresh and HMR 🔄

Astro comes with features like fast refresh and Hot Module Replacement (HMR), allowing you to see changes immediately after saving your files.

### Build Process 🚧

When you run pnpm run build, Astro doesn’t generate any JavaScript files by default. This reinforces Astro’s core idea: only load JavaScript when absolutely necessary.

**CSS Scoping**: Astro automatically creates a hash for the HTML elements based on the styles declared in your files. For example, if you style a `<main>` element within a component, Astro will ensure that style applies only to that specific `<main>` element, using a unique data attribute like `main[data-astro-cid-j7pv25f6]`.

## TailwindCSS Integration with Astro

Astro provides a seamless integration system where adding tools like tailwind is a simple as running a single command.

To explore all available integrations, you can use the following:

```bash
pnpm astro add --help
```

For example, to add TailwindCSS to your Astro project, you can run:

```bash
pnpm astro add tailwind
```

## Routing in Astro 🚦

Astro features a built-in routing system that works similarly to other frameworks.To create a new page, simply create a `.astro` file in the `pages` directory, and you can navigate to it by using the corresponding URL.

## Slots in Astro 🎛️

In a layout component like `Layout.astro`, you can use the `<slot />` element, which works similarly to `children` in React.

```astro
<slot />
```

### Named slots

Slots in Astro are a powerful feature that allows you to insert content into specific parts of a component. For example, if you want to add an icon to a button, either to the left or right, you can use named slots:

```astro
<slot name="before" /> <!-- This slot is placed BEFORE the button's text -->
```

You can then use this slot in another component:

```astro
<svg (...) slot="before"></svg> <!-- The SVG will appear BEFORE the text -->
```

> [!NOTE]
> This feature is similar to slots in Vue.js.

Layouts allow you to apply consistent styles and structure across all the content wrapped with the layout.

### Default Slot Content

If a slot does not receive any content, you can specify default content like this:

```astro
<slot>Default content</slot>
```

> [!INFO]
> This is a CSS Tip!
> Using the CSS property `color-scheme: dark light;` specifies that your site should default to dark mode, and all colors should adapt accordingly. For instance, text will be white without needing to explicitly set `color: #ffffff` or `text-white`.

## Markdown (.md) Support 📝

Astro fully supports Markdown files (`.md`). If you create a Markdown file in the `pages` directory, it will be accessible as a route, complete with default styles and formatting.

### Front Matter in Markdown

In Markdown, "Front Matter" refers to metadata at the top of a file enclosed in `---`. It is used to define variables that can be accessed within the Markdown file, such as the title, date, or layout.

```markdown
---
title: "My Markdown Page"
date: "2022-01-01"
layout: "Layout.astro"
---
```

## Content Collections 📚

Astro also supports a feature called Content Collections, which allows you to organize and manage your content more efficiently. This is an advanced feature worth exploring as you continue your Astro journey.

Additionally, you can create `.html` files in the `pages` directory, and they will be treated as routes just like `.astro` and `.md` files.

## Data Fetching

Fetching data in Astro is straightforward. Here’s an example of how to fetch data from an external API:

```astro
---
const res = await fetch('https://api.spacexdata.com/v5/launches');
const data = await res.json();
---
```

When working with fetched data in Astro, it’s important to note that the `console.log` statement won’t appear in the browser’s console. Instead, it will output in the VSCode terminal. This is because Astro does not execute JavaScript on the client by default. JavaScript execution happens either on the server-side or during the build process.

### Iterating Over Data

Unlike other frameworks, Astro does not require a key prop when iterating over elements. The iteration syntax may look similar, but its underlying functionality is different.

## Conditional Rendering 🎭

Astro offers a more declarative way to handle conditional rendering through the `class:list` directive. Instead of using a template string for conditional classes, you can use this utility to apply styles conditionally:

```astro
<span class:list={[
  "text-xs font-semibold mr-2 px-2.5 py-0.5 rounded",
  {
    "bg-green-400 text-green-900": success,
    "bg-red-400 text-red-900": !success
  }
]}>
  {successText}
</span>
```

This approach allows for a cleaner and more maintainable codebase.

## 404 Pages 🚫

Astro automatically handles 404 pages by generating a default 404 page if a route does not match any existing file. You can customize the 404 page by creating a `404.astro` file in the `src/pages/ directory`. This file will be served whenever a user navigates to a non-existent route.

```astro
// src/pages/404.astro
---
import Layout from '../layouts/Layout.astro';
---
```

## Dynamic Routes 🛤️

Astro allows you to create dynamic routes using a specific file naming convention:

File Naming Convention: Use square brackets [] in the file name to denote a dynamic route, like [id].astro.

### Static Routes

Astro can pre-generate dynamic routes using the getStaticPaths() function. This approach is ideal when you know all the pages or products you want to serve, and they are limited.

```astro
---
export async function getStaticPaths() {
  // Static paths
  return [
    { params: { id: '1' } },
    { params: { id: '2' } },
    // More static paths
  ];
}
---
```

### Dynamic Routes

For pages that change frequently or are generated dynamically, you can map over a list of items to create routes:

```astro
---
export async function getStaticPaths() {
  const launches = await getLaunches();

  return launches.map(launch => ({
    params: { id: launch.id }
  }));
}
---
```

### SSR (server-side rendering)

For truly dynamic content that needs to be updated frequently, you can use SSR. In your astro.config.mjs, set the output property to 'server':

```astro
export default defineConfig({
  integrations: [tailwind()],
  output: 'server'
});
```

#### Output Options

- **Server**: renders on demand by default. Use this when most or all of your site should be server-rendered on request.
- **Hybrid**: pre-renders to HTML by default. Use this when most of your site should be static. Individual pages or endpoints can opt out of pre-rendering using: `export const prerender = false;`.

## View Transitions 🎥

Astro supports view transitions, which you can implement using:

```astro
import { ViewTransitions } from "astro:transitions";
```

## Interactive Components (Islands)

By default, components in Astro are static. To make them interactive, you need to specify a directive using `client`.

### Client Directive

The `client` directive tells Astro to load the component on the client-side only when it's needed. This helps reduce the initial JavaScript payload and improves performance.

#### Options

- `client:load`
- `client:idle`
- `client:visible`
- `client:media`
- `client:only`

```astro
<SomeComponent client:visible />
```

## Persistence of Information 💾

When using `transition:persist`, Astro will persist information across navigations and animations. However, note that this doesn’t save data to localStorage, so the information will be lost if the page is refreshed.
