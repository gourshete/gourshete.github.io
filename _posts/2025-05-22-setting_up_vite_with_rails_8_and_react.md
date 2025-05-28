---
layout: post
title:  "Setting up Vite with Rails 8 and React"
date:   2025-05-22
keywords: "ruby rails react vite"
image: assets/images/vite-rails.png
categories: [ Rails, React, Vite]
---

<br>

# Setting up Vite with Rails 8 and React: A Complete Setup Guide

In this guide, we’ll go **step by step** from creating a new Rails app to rendering a simple "Hello from React" text in the browser using Vite for frontend tooling.


---

## Prerequisites

Before diving into setting up Vite with Rails and React, ensure your system has the following tools installed. These are essential to create and run the application smoothly.

---

#### 1. Ruby (Version 3.1 or higher recommended)
Ruby is the core language for Rails. You can check your installed version using:

```bash
ruby -v
```

If Ruby is not installed, consider using a version manager like [`rbenv`](https://github.com/rbenv/rbenv) or [`rvm`](https://rvm.io/) to manage versions:

```bash
brew install rbenv
rbenv install 3.2.2
rbenv global 3.2.2
```

---

#### 2. Rails (Version 7.1 or higher recommended)
Rails is the web framework we'll be using. Make sure it’s installed:

```bash
gem install rails
```

Confirm the installation with:

```bash
rails -v
```

---

#### 3. Node.js (Version 18+ required by Vite)
Vite requires a recent version of Node (v18 or newer). You can check the current version:

```bash
node -v
```

If you're not on the right version, use **nvm** to manage Node versions easily.

[`nvm`](https://github.com/nvm-sh/nvm) allows you to switch between multiple Node.js versions easily. This is useful if you’re working on multiple projects with different requirements.

Install `nvm`:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

Reload your shell (`.zshrc`, `.bashrc`, or `.bash_profile`), then install Node 18:

```bash
nvm install 18
nvm use 18
```


---

#### 4. Yarn (Package Manager for Node)
Yarn is used to manage JavaScript dependencies like React and Vite plugins. Install it via Homebrew (on macOS):

```bash
brew install yarn
```

Verify the installation:

```bash
yarn -v
```

---

#### 5. PostgreSQL (or another preferred DB)
Rails supports several databases, but PostgreSQL is widely used in production. You can install it in simple steps using [postgresapp.com](https://postgresapp.com/)

Ensure it's running correctly:

```bash
psql --version
```

You may also use SQLite (the Rails default), but PostgreSQL is recommended for most setups.

---

## Step-by-Step Setup

### 1. Create a New Rails 8 App with Vite

```bash
rails new vite-rails-app --javascript vite
cd vite-rails-app
```

This sets up your Rails app with Vite instead of the default import maps or Webpacker.

### 2. Add React to Your Project

Install React and ReactDOM using Yarn:

```bash
yarn add react react-dom
```

---

## Set Up React with Vite

### 3. Update `vite.config.ts`

Edit `vite.config.ts` to enable JSX support and React plugin:

```ts
import { defineConfig } from 'vite'
import RubyPlugin from 'vite-plugin-ruby'
import react from '@vitejs/plugin-react'

export default defineConfig({
  plugins: [
    RubyPlugin({
      additionalEntrypoints: ['**/*.jsx'],
    }),
    react(),
  ],
  server: {
    port: 3001
  }
})
```

---

## Set Up Rails View and Controller

### 4. Generate a Controller

```bash
rails generate controller Welcome index
```

This creates a `WelcomeController` with an `index` action and view.

### 5. Set Root Route

Edit `config/routes.rb`:

```rb
root "welcome#index"
```

---

## Create React Entry Point

### 6. Create `app.jsx`

Create the file: `app/frontend/entrypoints/app.jsx`

```jsx
import React from "react"
import ReactDOM from "react-dom/client"

const App = () => <h1>Hello from React!</h1>

const root = document.getElementById("root")
if (root) {
  ReactDOM.createRoot(root).render(<App />)
}
```

> ⚠️ Ensure the file has a `.jsx` extension so Vite can parse it correctly.

---

## Update Rails View to Load React

Edit `app/views/welcome/index.html.erb`:

```erb
<%= vite_client_tag %>
<%= vite_javascript_tag 'app' %>

<div id="root"></div>
```

This sets up the HTML and loads your React component inside the `#root` div.

---

## Run the App

### 7. Start Rails and Vite Dev Servers

In **one terminal**, run:

```bash
bin/rails server
```

In a **second terminal**, run:

```bash
bin/vite dev
```

Visit [http://localhost:3000](http://localhost:3000) — you should see:

```
Hello from React!
```

---

### Issues you might face -

#### `@vitejs/plugin-react can't detect preamble`
- Ensure you're using `.jsx` extension.
- Verify correct entrypoint name in `vite_javascript_tag`.

#### File not found in manifests
- Double-check file is inside `app/frontend/entrypoints`.
- File extension should be `.jsx`.

---

## Summary

You now have:

- A Rails 8 app
- React integrated via Vite
- Working React component rendered from a Rails view

This setup gives you the best of both worlds: Rails' robust backend and Vite's lightning-fast front-end tooling.

