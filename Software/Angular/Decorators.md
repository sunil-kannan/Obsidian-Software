---
date: "2025-10-15"
tags: 
link:
---

### 🚀 **Decorators in Angular**

A **decorator** is a **special type of function** in TypeScript that can be applied to classes, methods, properties, or parameters to **add metadata** and sometimes modify behavior.

In Angular, decorators are used for defining the **metadata** associated with various elements like components, services, directives, pipes, etc.

### 🧠 **Metadata**

**Metadata** refers to the **data about data** — in this case, **information about the class, method, property, or parameter** that the decorator is attached to. This metadata typically provides Angular with information about how to **configure** and **interact with** that class or its members.

### Class decorators, e.g. @Component and @NgModule

```ts
import { NgModule, Component } from '@angular/core';

@Component({
  selector: 'my-component',
  template: '<div>Class decorator</div>',
})
export class MyComponent {
  constructor() {
    console.log('Hey I am a component!');
  }
}

@NgModule({
  imports: [],
  declarations: [],
})
export class MyModule {
  constructor() {
    console.log('Hey I am a module!');
  }
}
```

### Property decorators Used for properties inside classes, e.g. @Input and @Output

```ts

import { Component, Input } from '@angular/core';

@Component({
    selector: 'my-component',
    template: '<div>Property decorator</div>'
})

export class MyComponent {
    @Input()
    title: string;
}
```

### Method decorators Used for methods inside classes, e.g. @HostListener

```ts
import { Component, HostListener } from '@angular/core';

@Component({
    selector: 'my-component',
    template: '<div>Method decorator</div>'
})
export class MyComponent {
    @HostListener('click', ['$event'])
    onHostClick(event: Event) {
        // clicked, `event` available
    }
}
```
### Parameter decorators Used for parameters inside class constructors, e.g. @Inject, @Optional

```ts
import { Component, Inject } from '@angular/core';
import { MyService } from './my-service';

@Component({
    selector: 'my-component',
    template: '<div>Parameter decorator</div>'
})
export class MyComponent {
    constructor(@Inject(MyService) myService) {
        console.log(myService); // MyService
    }
}

// Angular v18 and above

import { Component, inject } from '@angular/core';
import { MyService } from './my-service';

@Component({
    selector: 'my-component',
    template: '<div>Parameter decorator</div>'
})
export class MyComponent {
myService: MyService = inject(MyService)
    constructor() {
        console.log(myService); // MyService
    }
}

```


