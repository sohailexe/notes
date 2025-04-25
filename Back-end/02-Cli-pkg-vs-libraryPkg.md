# Node.js Packages, ES Modules, and CLI Tools

## 1. Enabling ES Module Imports

By default, Node.js treats `.js` files as CommonJS modules (using `require`). To use `import`/`export` syntax:

1. In your **package.json**, add:
   ```json
   {
     "type": "module"
   }
   Now you can write:
   ```

js
Copy code
// app.js
import express from 'express';

const app = express();
app.listen(3000, () => console.log('Server running')); 2. Library Packages vs. CLI Packages
Library packages

Installed via npm install <pkg> (or yarn add <pkg>).

Used inside your code (import or require).

Live under node_modules/<pkg>/.

CLI (command-line) packages

Installed via npm install <pkg> --save-dev (commonly) or npm install <pkg> -g.

Provide executable commands you run in your terminal.

Their executables are symlinked into node_modules/.bin/.

3. Using node_modules/.bin
   When you install a CLI tool locally:

bash
Copy code
npm install vite --save-dev
The vite executable ends up at node_modules/.bin/vite.

You can run it directly:

bash
Copy code
./node_modules/.bin/vite 4. npm Scripts vs. Direct Invocation vs. npx
4.1 npm Scripts
Define scripts in package.json:

json
Copy code
{
"scripts": {
"dev": "vite",
"build": "vite build"
}
}
Run with:

bash
Copy code
npm run dev
npm automatically adds node_modules/.bin to your PATH when running scripts.

4.2 Direct Invocation
Typing vite in your shell only works if:

You installed it globally (npm install -g vite), or

Your shell PATH includes ./node_modules/.bin.

4.3 npx
npx <cmd> will look for the command in:

Local node_modules/.bin

Global installs

Fallback to fetching from the registry

Example:

bash
Copy code
npx vite 5. What Does Vite Do?
Development server

Serves your project from the current directory.

Watches files and supports hot module replacement (HMR), like a “live server.”

Build tool

Bundles your code for production (vite build).

Optimizes assets (JS, CSS, images).

6. dependencies vs. devDependencies
   dependencies

Required at runtime (e.g., Express, React).

Installed with npm install <pkg>.

devDependencies

Required only during development or build (e.g., Vite, ESLint, Jest).

Installed with npm install <pkg> --save-dev.

Quick Example
bash
Copy code

# 1. Initialize

npm init -y

# 2. Enable ES modules

# (add "type": "module" to package.json)

# 3. Install dependencies

npm install express

# 4. Install dev tools

npm install vite --save-dev

# 5. Add scripts

# in package.json:

# "scripts": {

# "start": "node app.js",

# "dev": "vite"

# }

# 6. Run

npm run dev # starts Vite dev server
npm start # runs your Node.js app
npx vite # alternative to npm run dev
This setup lets you:

Use import/export in Node modules.

Keep build tools and CLI utilities in devDependencies.

Run everything smoothly via npm scripts or npx.
