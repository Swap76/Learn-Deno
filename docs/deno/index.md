# All About Deno

Deno is a secure TypeScript runtime built on V8, the Google runtime engine for JavaScript.

## Built with:

- Rust (Deno’s core was written in Rust, Node’s in C++)
- Tokio (the event loop written in Rust)
- TypeScript (Deno supports both JavaScript and TypeScript out of the box)
- V8 (Google’s JavaScript runtime used in Chrome and Node, among others)

## First-class TypeScript support

Deno is written in Rust and TypeScript, two of the languages that today are really growing fast.

In particular being written in TypeScript means we get a lot of the benefits of TypeScript even if we might choose to write our code in plain JavaScript.

And running TypeScript code with Deno does not require a compilation step - Deno does that automatically for you.

You are not forced to write in TypeScript, but the fact the core of Deno is written in TypeScript is huge.

The V8 JavaScript engine has a feature called V8 Snapshots that allows V8 to start up very quickly. Deno performs the same trick with the TypeScript compiler so it does not need to recompile the TypeScript compiler every time, giving you ultra-fast start-up times.

## Secure by default

While the V8 JavaScript engine is a sandboxed environment, Node.js pokes holes out of the sandbox to the operating system so it can perform operations on the operating system (OS), such as write files, read files, read and write environment variables, etc…

By default, Deno has the holes from the V8 Engine to the underlying OS closed. To give your program access to the operating system, Deno has a set of flags to run the program with.

```sh
--allow-net=www.example.com // url optional
--allow-read=/path // path optinal
--allow-write=/path // path optional
--allow-run
--allow-env
```

## Module imports

Deno introduces a completely new way of managing modules. Where Node.js has a bloated package.json file a lock file, Deno has code. Like the web, Deno has no centralized package repository, such as NPM. Instead, files are imported where needed and downloaded when they do not exist in the module cache.

```ts
import { serve } from "https://deno.land/std@0.50.0/http/server.ts";

for await (const req of serve({ port: 8000 })) {
  req.respond({ body: "Hello World\n" });
}
```

## Support for top-level await

Top-level await allows you to await an asynchronous function outside of an async function.

```ts
for await (const req of s) {
  req.respond({ body: "Hello World\n" });
}
```

## Browser-compatible events

Deno uses bowser-compatible APIs. One of the most exciting additions to the Deno API is a window object, making server-side modules even more compatible with client-side modules.
Compatibility with the browser, where possible, is one of Deno’s primary goals. This helps full-stack developers reduce context switching and making learning the two technologies easier.

## Built-in testing library

Having a good testing environment is a key part of creating good quality code. The JavaScript testing ecosystem has developed a lot in the last few years. However, it can still be painful to set up a testing environment that encourages the developer to write good quality tests.
Deno comes with a [built-in testing library](https://deno.land/std/testing) that aims to make testing easier and more consistent.

## HTTP Server Performance

The performance of [Deno's HTTP server](https://deno.land/benchmarks). A hello-world Deno HTTP server does about 25k requests per second with a max latency of 1.3 milliseconds. A comparable Node program does 34k requests per second with a rather erratic max latency between 2 and 300 milliseconds.

Deno's HTTP server is implemented in TypeScript on top of native TCP sockets. Node's HTTP server is written in C and exposed as high-level bindings to JavaScript. We have resisted the urge to add native HTTP server bindings to Deno, because we want to optimize the TCP socket layer, and more generally the op interface.

Deno is a proper asynchronous server and 25k requests per second is quite enough for most purposes. (If it's not, probably JavaScript is not the best choice.) Furthermore, Deno is expected to generally exhibit better tail latency due to the ubiquitous use of promises. There are more performance wins to be had in the system, and Deno will achieve that in future releases.
