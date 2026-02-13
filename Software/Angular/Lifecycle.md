---
date: "2026-02-13"
tags: 
link:
---

# Lifecycle

> The Angular component lifecycle is a series of stages that an instance goes through from creation to destruction. Developers can "hook into" these key moments using specific lifecycle hook methods to perform tasks like initialization and cleanup.


### Initialization and Change Detection

These hooks are called during the initial rendering and subsequent change detection cycles.

- **`ngOnChanges()`**: Called whenever Angular sets or resets data-bound **input properties** (`@Input()`). It receives a `SimpleChanges` object with current and previous values. This runs before `ngOnInit()` and can run many times after.
- **`ngOnInit()`**: Called once after the first `ngOnChanges()`. This is a good place for component initialization logic, such as fetching data from a server, as input properties are available at this point.
- **`ngDoCheck()`**: Called immediately after `ngOnChanges()` and `ngOnInit()` on the first run, and then during every subsequent change detection run. It is used to detect and act upon changes that Angular might not catch on its own, but should be used with caution due to its high frequency of calls. 

### Content and View Initialization

These hooks are specific to components (not directives) and deal with the initialization and checking of projected content and the component's own views. 

- **`ngAfterContentInit()`**: Called once after Angular projects external content into the component's view using `<ng-content>`.
- **`ngAfterContentChecked()`**: Called after `ngAfterContentInit()` and every subsequent `ngDoCheck()`. It's used to respond after the projected content has been checked for changes.
- **`ngAfterViewInit()`**: Called once after Angular initializes the component's views and child views. This is the time to access elements queried with `@ViewChild` or `@ViewChildren` and interact with the DOM.
- **`ngAfterViewChecked()`**: Called after `ngAfterViewInit()` and every subsequent `ngAfterContentChecked()`. It's used to respond after the component's views have been checked for changes. 

### Destruction

This hook is used for cleanup before the component is removed from the DOM. 

- **`ngOnDestroy()`**: Called immediately before Angular destroys the component or directive. This is the crucial place to put cleanup logic to prevent memory leaks, such as unsubscribing from Observables, detaching event handlers, and stopping timers.