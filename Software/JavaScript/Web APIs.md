---
date: 2024-10-30
tags: 
link:
---

# Web APIs

>A Web API is an application programming interface (API) for web. The concept of the Web API is not limited to JavaScript only. It can be used with any programming language. Let’s learn what web API is first.

When running JavaScript in the browser, you have access to various Web APIs provided by the browser itself, such as `fetch` for network calls, `setTimeout` for scheduling, and `localStorage` for storing data. These APIs allow you to perform asynchronous operations like network requests, timers, and more without blocking the main thread.

## JavaScript Web API List

Here, we have listed the most common web APIs.

| API                      | Description                                                              |
| ------------------------ | ------------------------------------------------------------------------ |
| Console API              | It is used to interact with the browser’s console.                       |
| Fetch API                | It is used to fetch data from web servers.                               |
| FullScreen API           | It contains various methods to handle HTML elements in full-screen mode. |
| GeoLocation API          | It contains the methods to get the user’s current location.              |
| History API              | It is used to navigate in the browser based on the browser’s history.    |
| MediaQueryList API       | It contains methods to query media.                                      |
| Storage API              | It is used to access the local and session storage.                      |
| Forms API                | It is used to validate the form data.                                    |
| setTimeout / setInterval | Schedule code to run after a delay or at regular intervals.              |
### Node.js vs. Browser Web APIs

Node.js also has Web APIs for asynchronous operations but with a focus on server-side tasks. For instance:

- Instead of `fetch`, Node.js uses libraries like `http` or `axios` (or `fetch` with newer Node.js versions).
- Node.js has additional APIs for filesystem access, process management, etc., which are specific to server environments.