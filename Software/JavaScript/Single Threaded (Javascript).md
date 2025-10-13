---
date: 2024-10-30
tags: 
link: "[[JavaScript]]"
---

# JavaScript: Is it Really Single-Threaded? 🤔

> Yes and no. It's a bit of a paradox.


## 📌 Single-Threaded Nature of JavaScript

JavaScript code itself is executed sequentially on a single thread (the main thread). However, the runtime environment (browser or Node.js) utilizes additional threads for [[Web APIs]] and potentially worker threads, allowing certain tasks to run in parallel.

## Understanding JavaScript's Execution Model

- **JavaScript operates on a single thread of execution.**  
  Only one piece of JavaScript code can be actively executing at any given moment.

### 👉 A Bit of History

- **Early Web:** In the beginning, browsers were simpler, and JavaScript was mainly used for adding interactivity to web pages.
- **Single-Threaded Model:** A single-threaded model was sufficient and helped keep the language implementation simpler, reducing concurrency issues like race conditions.

## 📌 What Creates the Illusion of Concurrency?

The **Event Loop** is what makes JavaScript feel concurrent. Think of it as a continuous cycle that manages asynchronous tasks without blocking the main thread.

## 📌 How It Works: Step-by-Step

1. **Function Execution:**  
   When you call a function, JavaScript's main thread starts executing it step-by-step.

2. **Offloading Tasks:**  
   If the function requires a time-consuming task (like a network request or a timer), it hands the task off to special helpers called [[Web APIs]] .

3. **Background Processing:**  
   Web APIs work in the background, performing the task without holding up the main thread.

4. **Callback Preparation:**  
   Before starting, the Web API asks for a "callback" – instructions on what to do once the task completes.

5. **Event Queue:**  
   When the Web API finishes, it places the callback in a waiting line called the **event queue**.

6. **The Event Loop:**  
   JavaScript has a special mechanism called the **event loop**. It constantly checks if the main thread is free.

7. **Executing Callbacks:**  
   If the main thread is idle and there are callbacks in the event queue, the event loop places the first callback onto the main thread.

8. **Callback Execution:**  
   The main thread executes the callback, following the instructions on how to handle the task's result.

This cycle repeats continuously.

## 📌 Summarizing It All

JavaScript’s single thread executes code line by line but achieves concurrency by offloading tasks (like timers or network requests) to Web APIs. These APIs manage tasks separately and return results to the event loop, which eventually executes them on the main thread.

**Note:** The event loop itself is not a separate thread. It runs on the main thread. When a function is being executed, the event loop waits until the main thread is free.

This is how JavaScript maintains concurrency on a single thread. 😉

---

Hope this helps clarify the workings of JavaScript's single-threaded nature and how it achieves concurrency!
