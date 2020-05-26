# Background

## Why Deno? Is it needed?

Deno was announced almost 2 years ago by the Node.js original creator Ryan Dahl at JSConf EU. Watch the [YouTube video](https://www.youtube.com/watch?v=M3BM9TB-8yA) of the talk, it’s very interesting and it’s a mandatory watch if you are involved in Node.js and JavaScript in general.

Every project manager must take decisions. Ryan regretted some early decisions in Node. Also, technology evolves, and today JavaScript is a totally different language than what it was back in 2009 when Node started. Think about the modern ES6/2016/2017 features, and so on.

So he started a new project to create some sort of second wave of JavaScript-powered server side apps.

## Will it replace Node.js?

No. Node.js is a giant, well established, incredibly well supported technology that is going to stay for decades.

# NodeJS vs Deno Comparison

## Similarities

- Both are developed upon the V8 Chromium Engine
- Both are great for developing server-side with JavaScript

## Differences

- Node is written in C++ and JavaScript. Deno is written in Rust and TypeScript.
- Node has an official package manager called npm. Deno does not, and instead lets you import any ES Module from URLs.
- Node uses the CommonJS syntax for importing pacakges. Deno uses ES Modules, the official way.
- Deno uses modern ECMAScript features in all its API and standard library, while Node.js uses a callbacks-based standard library and has no plans to upgrade it.
- Deno offers a sandbox security layer through permissions. A program can only access the permissions set to the executable as flags by the user. A Node.js program can access anything the user can access
- Deno has for a long time envisioned the possibility of compiling a program into an executable that you can run without external dependencies, like Go, but it’s still not a thing yet. That’d be a game changer.

## Feature wise comparison

Node and Deno were built to serve the same purpose. That provides us a foundational common ground for comparison.

| Features                  | Node                   | Deno                |
| ------------------------- | ---------------------- | ------------------- |
| Engine                    | Chrome V8              | Chrome V8           |
| Uses                      | JavaScript             | TypeScript          |
| Written in                | C++ & Libuv            | Rust & Tokio        |
| Security                  | full-access            | explicit-access     |
| Package Managing          | npm                    | absolute url-based  |
| Importing with Extensions | optional; non-explicit | mandatory; explicit |
| Module Ecosystem          | CommonJS               | ES moduling         |
| Browser Support           | ambiguous; vague       | supported           |
| Native Async Programming  | Callbacks              | Promises            |
| Unhandled Promises        | uncaught exceptions    | dies immediately    |
| ECMAScript Support        | not built-in           | built-in            |
| TypeScript Support        | not built-in           | built-in            |
| Code Formatting           | not built-in           | built-in            |
| Top-Level Await           | not built-in           | built-in            |
