---
date: "2025-10-15"
tags: 
link:
---

# Metadata

> Metadata is used to decorate a class so that it can configure the expected behavior of the class. The metadata is represented by decorators.






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

Property decorators Used for properties inside classes, e.g. @Input and @Output
import { Component, Input } from '@angular/core';

@Component({
    selector: 'my-component',
    template: '<div>Property decorator</div>'
})

export class MyComponent {
    @Input()
    title: string;
}
Method decorators Used for methods inside classes, e.g. @HostListener
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
Parameter decorators Used for parameters inside class constructors, e.g. @Inject, @Optional
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




