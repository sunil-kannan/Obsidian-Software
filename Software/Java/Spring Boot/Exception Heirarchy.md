---
date: 2024-12-03
tags: 
link:
---


# Exception Heirarchy

> A blog is just like having a long conversation with people, so it should make sense that things you enjoy talking about will be closely related to your passion.

1. Any Exception?
   └──> HandlerExceptionResolverComposite
          (Flow from Left to Right)
          ├──> ExceptionHandlerExceptionResolver
          │       - Handles exceptions defined with @ControllerAdvice and @ExceptionHandler
          │       - If exception is handled → Goes to DefaultErrorAttributes
          │       - If exception is NOT handled → Passes to the next resolver
          │
          ├──> ResponseStatusExceptionResolver
          │       - Checks for exceptions with @ResponseStatus annotation
          │       - If exception is handled → Goes to DefaultErrorAttributes
          │       - If exception is NOT handled → Passes to the next resolver
          │
          └──> DefaultHandlerExceptionResolver
                  - Handles default Spring framework exceptions
                  - If exception is handled → Goes to DefaultErrorAttributes
                  - If exception is NOT handled → Returns a default response
              
2. DefaultErrorAttributes → Generates the error response.

![[exception hierarchy in springboot.png]]