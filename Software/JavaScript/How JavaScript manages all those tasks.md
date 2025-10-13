---
date: 2024-10-25
tags: 
link: "[[JavaScript]]"
---

# How JavaScript manages all those tasks

> Ever wondered how javascript manages all those tasks?

![[javascript single threaded.png]]


> Does the event loop run on same thread as the JS main thread?

JavaScript is often called single threaded, because different pieces of JavaScript can't run at the same time. (Although with the introduction of [Web Workers](https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API), this isn't necessarily true anymore.) Whether you call this the "main" thread depends on your definition of "main". If you are asking about whether the event loop itself runs on the same thread as the messages it executes, than that would make sense, but this is implementation dependent.

JavaScript doesn't dictate any threading at all. It makes sense for implementations to use only a one thread for the event loop and the JavaScript execution because all the code will always run sequentially, but this isn't a requirement.

As for your questions about event loop and the call stack, you first need to understand how those two work.

The event loop is a simple mechanism that executes queued messages in order and if none are available, it will wait until a new one comes in. A message can be anything that isn't executed immediately. Such as (but not limited to) incoming events (such as clicks), responses from AJAX calls or a callback from `setTimeout()`.

The call stack is the stack of function calls. When a function is invoked (directly, so not via the event loop), a new frame is added to the stack that will be executed. Once the function has completed, the frame is removed from the stack and the code of the previous frame will continue from the point it invoked the completed function. Once all functions are complete and the call stack is empty, the event loop will run the next message.

So to answer your remaining questions:

> does all synchronous code in `Main()` have to go through the event loop?

Not directly. The event loop only invokes the message and wait for it to complete. It doesn't interfere with the execution of the message itself.

> is the event loop the only one who is allowed to push functions to call stack?

The only time the event loop interacts with the call stack (or the "execution context stack" as the specification calls it), is when it "[spins the event loop](https://html.spec.whatwg.org/multipage/webappapis.html#spin-the-event-loop)". In such a case, the call stack is copied for later use, some other task is performed and later the copied call stack is restored so the execution can continue from the point it left off. But this only happens on a handful of occasions.

Generally, frames are added to the call stack when a (synchronous) function is called. The event loop has little to do with that.

### Key Takeaways:

- The **main thread executes both synchronous (call stack) and asynchronous (event loop) tasks**.
- The **event loop runs only when the call stack is empty**.
- The **main thread "drives" the event loop**, meaning it checks the event queue only when it's not busy with synchronous code.
- **Since JavaScript is single-threaded, only one thing runs at a time**—either a function from the call stack or an asynchronous task from the event queue.