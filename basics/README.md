# Astro Basics 🪐

This README ccontains theoretical notes and key concepts to understand Astro.

> ![WARNING]
> Maybe some of the concepts are not 100% accurate because I'm just starting to learn Astro. If you find any mistakes, please let me know!

## Table of Contents

- [What is Astro?](#what-is-astro)

## Island Architecture 🏝

**Island Architecture** is a frontend design pattern where static pages contain "islands" of interactivity. These islands are reactive components that load JavaScript only when necessary, enhancing performance by reducing the amount of JavaScript loaded by default.

### Why Does It Matter?

- **Performance**: by not loading JavaScript on the client by default, pages load faster, improving user experience.
- **SEO**: static content is easily indexable by search engines, ensuring better SEO performance.
- **Framework Agnostic**: Astro allows you to use multiple UI libraries like React, Vue, Svelte, or Angular in the same project, providing flexibility in choosing the best rools for you needs.

> ![NOTE]
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
- **Components**: Astro minimizes boilerplate, enabling you to write less code while achieving the same functionality.

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

> ![NOTE]
> Fun fact! Astro uses port 4321 for its dev server, like a countdown to a rocket launch!

## Fast Refresh and HMR 🔄

Astro comes with features like fast refresh and Hot Module Replacement (HMR), allowing you to see changes immediately after saving your files.

### Build Process 🚧

When you run pnpm run build, Astro doesn’t generate any JavaScript files by default. This reinforces Astro’s core idea: only load JavaScript when absolutely necessary.

**CSS Scoping**: Astro automatically creates a hash for the HTML elements based on the styles declared in your files. For example, if you style a `<main>` element within a component, Astro will ensure that style applies only to that specific `<main>` element, using a unique data attribute like `main[data-astro-cid-j7pv25f6]`.
