# Angular_Elements

https://angular.io/guide/elements

In Angular, "elements" refer to custom HTML elements that are created and used within an Angular application. These elements are also known as Angular Elements or Angular Custom Elements. They allow you to encapsulate Angular components and use them in non-Angular applications or frameworks, such as plain HTML, React, or Vue.

Angular Elements are created by compiling an Angular component into a standalone JavaScript bundle. This bundle can then be included in any HTML page, and the custom element can be used like any other HTML element.

Here's a simple code sample that demonstrates the creation of an Angular Element:

## 1. Create an Angular component:

```typescript
import { Component, Input } from '@angular/core';

@Component({
  selector: 'my-element',
  template: `
    <h1>{{ message }}</h1>
    <p>Counter: {{ counter }}</p>
    <button (click)="increment()">Increment</button>
  `,
})
export class MyElementComponent {
  @Input() message: string;
  counter: number = 0;

  increment() {
    this.counter++;
  }
}
```

## 2. Create an Angular module and define the component as an entry component:

```typescript
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { createCustomElement } from '@angular/elements';
import { MyElementComponent } from './my-element.component';

@NgModule({
  imports: [BrowserModule],
  declarations: [MyElementComponent],
  entryComponents: [MyElementComponent],
})
export class AppModule {
  constructor() {
    const myElement = createCustomElement(MyElementComponent, { injector: this.injector });
    customElements.define('my-element', myElement);
  }

  ngDoBootstrap() {}
}
```

## 3. Bootstrap the Angular module (main.ts):

```typescript
import { platformBrowserDynamic } from '@angular/platform-browser-dynamic';
import { AppModule } from './app.module';

platformBrowserDynamic().bootstrapModule(AppModule);
```

## 4. Build the Angular project as an Angular Element:

ng build --prod --output-hashing none --single-bundle true

This will generate a single JavaScript bundle (main.js) that includes the Angular Element.

## 5. Include the Angular Element in an HTML page:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Angular Element Demo</title>
</head>
<body>
  <my-element message="Hello Angular Element"></my-element>
  <script src="path/to/main.js"></script>
</body>
</html>
```

In this example, the MyElementComponent is transformed into an Angular Element using the createCustomElement function. The Angular module is bootstrapped with the ngDoBootstrap method. Finally, the main.js bundle is included in an HTML page, and the my-element custom element is used with the message input property.

When the HTML page is loaded, the Angular Element will be rendered, and you'll see the message "Hello Angular Element" along with a counter that can be incremented by clicking the "Increment" button.

Note that Angular Elements require Angular version 6 or above and require additional setup steps for compatibility with different frameworks or environments.


