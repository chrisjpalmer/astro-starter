# Astro Starter Kit: Basics

## Hugo

Here's how you make it so you can pass the api url in as a URL.
The basic astro template won't work with environment variables as it is... you need to modify astro so it supports server side rendering.
Also you need to modify the dockerfile CMD section to host the site with the server side rendering server (not `serve`)

1. Follow this guide and mod your project: https://docs.astro.build/en/guides/deploy/kinsta/#ssr
2. Use an environment variable in your code (https://docs.astro.build/en/guides/environment-variables/). An example of me doing this is in index.astro.
   ```ts
    const apiUrl = import.meta.env.PUBLIC_APIURL;
   ```
3. Create a `.env` file in the root of your astro project (like not the folder that contains both the python and web folder, I meant the root of the web project.) 
4. Add this to `.env`:

```env
PUBLIC_APIURL=localhost:5000
```

3. Display it on the page for now so we can just test it works.

### Test it out locally

After doing the above steps 

1. `npm run build`
2. `npm run start` - this is using the new start command that was modified to essentially do server side rendering.

If you get an error while running, check that you did the above steps properly.

### Dockerfile modifications

1. There is no need for that `script/run.sh` I was about to make you do.
2. In the docker compose for the website container, add an envfile reference the `.env` file that we created in the first step

### Test it out dockerfile way

```
docker compose up
```

### Okay now wire up

Wire up the reference to the environment variable to all parts of your application that need the URL.

```Dockerfile

CMD ["npm", "run", "start"]
```

```sh
npm create astro@latest -- --template basics
```

[![Open in StackBlitz](https://developer.stackblitz.com/img/open_in_stackblitz.svg)](https://stackblitz.com/github/withastro/astro/tree/latest/examples/basics)
[![Open with CodeSandbox](https://assets.codesandbox.io/github/button-edit-lime.svg)](https://codesandbox.io/p/sandbox/github/withastro/astro/tree/latest/examples/basics)
[![Open in GitHub Codespaces](https://github.com/codespaces/badge.svg)](https://codespaces.new/withastro/astro?devcontainer_path=.devcontainer/basics/devcontainer.json)

> 🧑‍🚀 **Seasoned astronaut?** Delete this file. Have fun!

![just-the-basics](https://github.com/withastro/astro/assets/2244813/a0a5533c-a856-4198-8470-2d67b1d7c554)

## 🚀 Project Structure

Inside of your Astro project, you'll see the following folders and files:

```text
/
├── public/
│   └── favicon.svg
├── src/
│   ├── components/
│   │   └── Card.astro
│   ├── layouts/
│   │   └── Layout.astro
│   └── pages/
│       └── index.astro
└── package.json
```

Astro looks for `.astro` or `.md` files in the `src/pages/` directory. Each page is exposed as a route based on its file name.

There's nothing special about `src/components/`, but that's where we like to put any Astro/React/Vue/Svelte/Preact components.

Any static assets, like images, can be placed in the `public/` directory.

## 🧞 Commands

All commands are run from the root of the project, from a terminal:

| Command                   | Action                                           |
| :------------------------ | :----------------------------------------------- |
| `npm install`             | Installs dependencies                            |
| `npm run dev`             | Starts local dev server at `localhost:4321`      |
| `npm run build`           | Build your production site to `./dist/`          |
| `npm run preview`         | Preview your build locally, before deploying     |
| `npm run astro ...`       | Run CLI commands like `astro add`, `astro check` |
| `npm run astro -- --help` | Get help using the Astro CLI                     |

## 👀 Want to learn more?

Feel free to check [our documentation](https://docs.astro.build) or jump into our [Discord server](https://astro.build/chat).
