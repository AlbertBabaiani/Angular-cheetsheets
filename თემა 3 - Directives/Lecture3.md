# Angular Directives: A Comprehensive Guide

Directives are a fundamental feature of Angular that allow you to extend HTML with custom behavior and DOM manipulation capabilities.

Think of directives as instructions that tell Angular how to render a template in the DOM (Document Object Model).

## Types of Directives in Angular

There are three main types of directives in Angular:

- `Component Directives` - Directives with a template, essentially reusable UI components.
- `Structural Directives` - Modify the DOM structure by adding, removing, or replacing elements.
- `Attribute Directives` - Change the appearance or behavior of an existing element.
- Additionally, you can create Custom Directives to implement specific functionality tailored to your application.

## Structural Directives

Structural directives are responsible for HTML layout. They shape or reshape the DOM's structure, typically by **adding, removing, or manipulating elements**.

They are easy to recognize in a template **as they are prefixed with an asterisk (\*)**.

### Built-in Structural Directives

- `*ngIf` - Conditionally adds or removes an element from the DOM.
- `*ngFor` - Loops over a collection to render elements dynamically.
- `*ngSwitch` - Displays elements based on a condition (similar to a switch-case statement).

### 1. \*ngIf

The \*ngIf directive includes or excludes an element based on a condition.

```html
<div *ngIf="isLoggedIn">Welcome back, User!</div>
```

In this example, the `<div>` is only included in the DOM if `isLoggedIn` is true.

The `*ngIf` directive also supports an `else` clause:

```html
<div \*ngIf="isLoggedIn; else loggedOut">Welcome back, User!</div>
<ng-template #loggedOut>Please log in.</ng-template>
```

### 2. \*ngFor

The `*ngFor` directive repeats a portion of the DOM for each item in an iterable list.

```html
<ul>
  <li *ngFor="let item of items; let i=index">{{i + 1}} - {{item.name}}</li>
</ul>
```

#### Additional features of \*ngFor:

- `index`: The position of the current item.
- `first`: True if the current item is the first.
- `last`: True if the current item is the last.
- `even`: True if the current index is even.
- `odd`: True if the current index is odd.

Example with multiple local variables:

```html
<div \*ngFor="let item of items; let i=index; let isOdd=odd">
  <p [class.odd]="isOdd">{{i}} - {{item.name}}</p>
</div>
```

### Understanding `trackBy` in `*ngFor`

The `trackBy` function helps Angular identify which items in a collection have changed when the collection is updated. Without `trackBy`, Angular uses object identity to track changes, which can lead to unnecessary DOM manipulations and poor performance, especially with large lists.

#### Basic Usage

Here's how you implement a `trackBy` function:

```typescript
// In your component class
trackByFn(index: number, item: any): any {
  return item.id; // Use a unique identifier from your data
}
```

Then in your template:

```html
<div *ngFor="let item of items; trackBy: trackByFn">{{ item.name }}</div>
```

### Why `trackBy` Is Important

Without `trackBy`, if your collection changes (even if many of the items are the same), Angular will:

1. Remove all DOM elements associated with the old collection
2. Create new DOM elements for the new collection

This is inefficient when many elements haven't actually changed.

With `trackBy`, Angular can:

1. Identify which items existed in the previous collection
2. Reuse the DOM elements for those items
3. Only create/remove elements that actually changed

### Example: With and Without `trackBy`

Let's say you have a list of users that gets refreshed from an API:

```typescript
@Component({
  selector: "app-user-list",
  template: `
    <!-- Without trackBy -->
    <div>
      <h2>Without trackBy</h2>
      <div *ngFor="let user of users">
        {{ user.name }}
      </div>
    </div>

    <!-- With trackBy -->
    <div>
      <h2>With trackBy</h2>
      <div *ngFor="let user of users; trackBy: trackByUserId">
        {{ user.name }}
      </div>
    </div>

    <button (click)="refreshUsers()">Refresh Users</button>
  `,
})
export class UserListComponent {
  users: User[] = [
    { id: 1, name: "Alice" },
    { id: 2, name: "Bob" },
    { id: 3, name: "Charlie" },
  ];

  trackByUserId(index: number, user: User): number {
    return user.id;
  }

  refreshUsers(): void {
    // This creates new object references but with the same data
    this.users = [
      { id: 1, name: "Alice" },
      { id: 2, name: "Bob" },
      { id: 3, name: "Charlie" },
    ];
  }
}
```

In this example, without `trackBy`, clicking "Refresh Users" would cause Angular to recreate all DOM elements even though the data is identical. With `trackBy`, Angular would recognize that the objects are the same (by their IDs) and wouldn't make any DOM changes.

### Performance Considerations

The `trackBy` function should:

1. Be **fast** - it runs for every item in your collection
2. Return a **unique identifier** for each item
3. Return a **stable identifier** that doesn't change for the same logical item

### Common Patterns for `trackBy`

1. **Using a unique ID property**:

   ```typescript
   trackByUserId(index: number, item: User): number {
     return item.id;
   }
   ```

2. **Using multiple properties when no single ID exists**:

   ```typescript
   trackByComposite(index: number, item: Product): string {
     return `${item.category}-${item.name}`;
   }
   ```

3. **Using the index when items don't have unique identifiers**:
   ```typescript
   trackByIndex(index: number): number {
     return index; // Only use as a last resort
   }
   ```

### Best Practices

1. **Always use `trackBy` with large lists** (more than 10 items)
2. **Always use `trackBy` when lists can be updated**
3. **Choose a truly unique identifier** for tracking
4. **Keep the `trackBy` function simple** to avoid performance issues

### When Not to Use `trackBy`

You might skip `trackBy` when:

- The list is very small (fewer than 5 items)
- The list never changes during the component's lifetime
- Every item in the list is always completely replaced (no items persist between updates)

### Debugging `trackBy`

You can debug `trackBy` functions by logging which items are being tracked:

```typescript
trackByUserId(index: number, user: User): number {
  console.log(`Tracking user ${user.name} with ID ${user.id}`);
  return user.id;
}
```

### 3. \*ngSwitch

The \*ngSwitch directive displays one element from a set based on a condition.

```html
<div [ngSwitch]="userRole">
  <div *ngSwitchCase="'admin'">Admin panel</div>
  <div *ngSwitchCase="'user'">User dashboard</div>
  <div *ngSwitchDefault>Login page</div>
</div>
```

### How Structural Directives Work

Under the hood, Angular transforms the asterisk syntax into a more verbose form using `<ng-template>`. For example, this:

```html
<div *ngIf="isLoggedIn">Content</div>
```

becomes:

```html
<ng-template [ngIf]="isLoggedIn">
  <div>Content</div>
</ng-template>
```

## Attribute Directives

Attribute Directives modify the behavior or appearance of an existing DOM element without changing its structure.

Unlike structural directives (like *ngFor or *ngIf) which modify DOM layout, attribute directives enhance existing elements.

They are applied like HTML attributes.

### Common Attribute Directives

- `ngClass` - Dynamically adds or removes CSS classes.
- `ngStyle` - Dynamically applies inline styles.
- `ngModel` - Enables two-way data binding (requires FormsModule).

### ngClass

---

**Purpose:** Adds or removes CSS classes based on conditions.

**Syntax:** `[ngClass]="expression"`

**How it works:** The expression can be a **string, array, or object** that defines which classes to apply.

`app.component.html`:

```html
<div [ngClass]="{'highlight': isActive, 'dim': !isActive}">
  This text changes style!
</div>
```

`app.component.ts`:

```TS
export class AppComponent {
    isActive = true;
}
```

`app.component.css`:

```CSS
.highlight { background-color: yellow; }
.dim { background-color: gray; }
```

If `isActive` is true, the highlight class is applied (yellow background). If false, the dim class is applied (gray background).

### ngStyle

---

**Purpose:** Applies inline styles dynamically.

**Syntax:** `[ngStyle]="expression"`

**How it works:** The expression is an object where keys are CSS properties and values are dynamic.

`app.component.html`:

```html
<div [ngStyle]="{'color': isError ? 'red' : 'green', 'font-size.px': fontSize}">
  Styled text!
</div>
```

`app.component.ts`:

```TS
export class AppComponent {
    isError = false;
    fontSize = 20;
}
```

The text will be green if `isError` is false, red if true, and the font size will be 20px.

### ngModel

---

**Purpose:** Enables two-way data binding between an input and a component property.

**Syntax:** `[(ngModel)]="property"`

**How it works:** Updates the property when the input changes and vice versa.

`app.component.html`:

```html
<input [(ngModel)]="username" placeholder="Enter your name" />

<p>Hello, {{ username }}!</p>
```

`app.component.ts`:

```TS
export class AppComponent {
    username = '';
}
```

> Add FormsModule to your app.module.ts:

`app.component.module`:

```TS
import { FormsModule } from '@angular/forms';
@NgModule({
    imports: [FormsModule],
    // ...
})
```

## Inline Style Binding

Angular offers several powerful ways to manipulate styles directly in templates without creating custom directives.

### 1. Style Property Binding

The most direct way to change a single style property:

```html
<div [style.background-color]="'lightblue'">Background color binding</div>
```

With a dynamic value from component:

```html
<div [style.background-color]="highlightColor">Dynamically colored div</div>
```

### 2. Style Property Binding with Units

You can specify CSS units:

```html
<div [style.width.px]="containerWidth">Width in pixels</div>

<div [style.font-size.em]="fontSize">Text with dynamic size in em</div>

<div [style.height.%]="heightPercentage">Height in percentage</div>
```

### 3. Conditional Style Binding

Apply styles conditionally using the ternary operator:

```html
<div [style.color]="isError ? 'red' : 'green'">Conditional text color</div>
```

### 4. Multiple Style Properties with `ngStyle`

When you need to set multiple styles at once:

```html
<div
  [ngStyle]="{
  'background-color': backgroundColor,
  'font-size': fontSize + 'px',
  'font-weight': isBold ? 'bold' : 'normal'
}"
>
  Multiple styles at once
</div>
```

### 5. Binding to a Method

For complex style logic:

```html
<div [ngStyle]="getStyles()">Styles from method</div>
```

```typescript
getStyles() {
  return {
    'background-color': this.isDarkTheme ? '#333' : '#fff',
    'color': this.isDarkTheme ? '#fff' : '#333',
    'padding': this.isCompact ? '5px' : '15px',
    'border-radius': '4px'
  };
}
```

## Class Binding Techniques

Similar to style binding, class binding is useful for manipulating CSS classes:

### 1. Single Class Binding

Toggle a single class based on a condition:

```html
<div [class.active]="isActive">Active when isActive is true</div>
```

### 2. Multiple Classes with `ngClass`

Apply multiple classes conditionally:

```html
<div
  [ngClass]="{'active': isActive, 'disabled': isDisabled, 'highlight': isHighlighted}"
>
  Multiple conditional classes
</div>
```

With arrays:

```html
<div [ngClass]="['base-class', conditionalClass]">Array of classes</div>
```

With method:

```html
<div [ngClass]="getClasses()">Classes from method</div>
```

## When to Use Inline Style Binding vs. Custom Directives

### Use Inline Style Binding When:

- You need simple style changes based on component state
- The styling logic is specific to a single component
- You're making a few style changes in limited places

```html
<button
  [style.background-color]="isActive ? '#007bff' : '#6c757d'"
  [style.color]="isActive ? 'white' : '#333'"
>
  Toggle Button
</button>
```

## Combining Inline Styles with Custom Directives

You can also combine inline style binding with custom directives:

```html
<div
  appHighlight
  [highlightColor]="'yellow'"
  [style.border]="'1px solid black'"
  [style.padding.px]="20"
>
  Combined approach
</div>
```

## Real-World Example: Progress Bar

Here's an example of a progress bar using inline style binding:

```html
<div class="progress-container">
  <div
    class="progress-bar"
    [style.width.%]="progressValue"
    [style.background-color]="getColorForProgress()"
  >
    {{progressValue}}%
  </div>
</div>
```

```typescript
progressValue = 75;

getColorForProgress(): string {
  if (this.progressValue < 30) return '#dc3545'; // danger
  if (this.progressValue < 70) return '#ffc107'; // warning
  return '#28a745'; // success
}
```

With CSS:

```css
.progress-container {
  width: 100%;
  height: 20px;
  background-color: #e9ecef;
  border-radius: 4px;
  overflow: hidden;
}

.progress-bar {
  height: 100%;
  text-align: center;
  color: white;
  transition: width 0.3s ease;
}
```

## Performance Considerations

### Style Binding Performance Tips:

1. **Use class binding over style binding when possible** - It's generally more performant to toggle CSS classes than to manipulate inline styles.

1. **Avoid complex expressions in templates** - Move complex style logic to component methods.

1. **Be careful with frequent style updates** - Changing styles frequently can cause layout thrashing; consider using CSS animations instead.

## Best Practices

1. **Avoid overusing inline styles** - They can make templates harder to read and maintain. Consider component styles for most cases.

1. **Use meaningful component properties** - Name your properties clearly to make template bindings self-explanatory.

1. **Create custom directives for reusable style logic** - If you find yourself repeating the same style bindings, create a directive.

1. **Consider CSS variables for theme-related styles** - For theme-related styling that changes globally, CSS variables might be more appropriate.

1. **Prefer class binding for toggling pre-defined styles** - It's cleaner to define styles in CSS and toggle their application via class binding.

```html
<!-- Better -->
<div [class.highlight]="isHighlighted">Highlighted content</div>

<!-- Instead of -->
<div [style.background-color]="isHighlighted ? '#fff4cc' : 'transparent'">
  Highlighted content
</div>
```

## Component Directives

Component directives are the most common type of directive in Angular applications.

A component combines a template, styles, and a TypeScript class to create a reusable piece of UI.

**Component Directives are directives with a template.**

### Key Characteristics

- Defined with the @Component decorator.
- Automatically act as directives when used in templates.
- Have their own template
- Can have their own styles
- Can receive inputs and emit outputs
- Can have lifecycle hooks
- Follow a clear encapsulation

`app.component.ts`:

```TS
import { Component } from '@angular/core';

@Component({
    selector: 'app-greeting',
    template: '<p>Hello, {{ name }}!</p>',
    styles: ['p { color: blue; }']
})
export class GreetingComponent {
    name = 'Student';
}
```

`app.component.html`:

```HTML
<app-greeting></app-greeting>
```

The `<app-greeting>` tag acts as a directive, rendering "Hello, Student!" in blue text.

# Understanding Custom Angular Directives: A Step-by-Step Guide

## Table of Contents

1. [Introduction to Custom Directives](#introduction-to-custom-directives)
2. [Creating a Basic Custom Attribute Directive](#creating-a-basic-custom-attribute-directive)
3. [Understanding @Input in Directives](#understanding-input-in-directives)
4. [Input Name Overlapping](#input-name-overlapping)
5. [@HostBinding in Detail](#hostbinding-in-detail)
6. [@HostListener in Detail](#hostlistener-in-detail)
7. [Using Renderer2 for DOM Manipulation](#using-renderer2-for-dom-manipulation)
8. [Building a Practical Custom Attribute Directive](#building-a-practical-custom-attribute-directive)
9. [Creating Custom Structural Directives](#creating-custom-structural-directives)
10. [Real-World Examples](#real-world-examples)

## Introduction to Custom Directives

Custom directives in Angular allow you to create reusable behaviors that you can attach to elements in your templates.

They extend HTML with custom functionality and can help you avoid code duplication across your application.

There are two main types of custom directives you can create:

- **Attribute directives**: Change the appearance or behavior of an existing element
- **Structural directives**: Add, remove, or manipulate host elements in the DOM

## Creating a Basic Custom Attribute Directive

Let's start with creating a simple attribute directive to understand the fundamentals:

### Step 1: Generate a new directive using Angular CLI

```bash
ng generate directive highlight
# or shorter syntax
ng g d highlight
```

This creates two files:

- `highlight.directive.ts`: Contains the directive class
- `highlight.directive.spec.ts`: Contains tests for the directive

### Step 2: Implement the directive

Let’s start with a simple attribute directive that changes text color.

### Code:

```typescript
import { Directive, ElementRef } from "@angular/core";

@Directive({
  selector: "[appHighlight]", // The name you’ll use in HTML
})
export class HighlightDirective {
  constructor(private el: ElementRef) {
    // Apply a background color to the element
    this.el.nativeElement.style.backgroundColor = "yellow"; // Access the element and change its background color
  }
}
```

### Step 3: Use the directive in a template

```html
<p appHighlight>This text will have a yellow background</p>
```

- **Explanation**:
  - `ElementRef` gives you access to the DOM element where the directive is applied.
  - In the constructor, we set the background color to blue when the directive loads.

## Understanding @Input in Directives

The `@Input` decorator allows directives to accept configuration values from the parent component. This makes directives more flexible and reusable.

### Basic @Input Usage

Let's enhance our highlight directive to accept a color:

```typescript
import { Directive, ElementRef, Input, OnInit } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective implements OnInit {
  @Input() highlightColor = "yellow"; // Default color

  constructor(private el: ElementRef) {}

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor = this.highlightColor;
  }
}
```

Now we can use it like this:

```html
<p appHighlight highlightColor="lightblue">
  This will have a light blue background
</p>
```

### Why We Need @Input

The `@Input` decorator serves several important purposes:

1. **Communication**: It enables parent components to pass data to directives
2. **Configuration**: It allows directives to be customized for different use cases
3. **Reactivity**: Angular tracks changes to input properties and triggers updates accordingly

### Input Property Life Cycle

Understanding when input values are available is important:

1. In the `constructor`: Input values are NOT yet available
2. In `ngOnInit`: Input values are available
3. In `ngOnChanges`: You can react to input changes (including the first value)

## Input Name Overlapping

> Sometimes, you might want the input property name to match the directive selector name. This is called `input name overlapping` and it's a common source of confusion.

### The Problem

Consider our directive with selector `[appHighlight]`. What if we want to pass the color directly to the directive name instead of using a separate property?

```html
<!-- We want this: -->
<p [appHighlight]="'orange'">Orange background</p>

<!-- Instead of this: -->
<p appHighlight [highlightColor]="'orange'">Orange background</p>
```

### The Solution: Input Aliasing

Angular allows you to alias an input property to match the selector:

```typescript
import { Directive, ElementRef, Input, OnInit } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective implements OnInit {
  // The input property name is 'appHighlight' but we store it in the 'highlightColor' property
  @Input("appHighlight") highlightColor = "yellow";

  constructor(private el: ElementRef) {}

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor = this.highlightColor;
  }
}
```

Now you can use it like this:

```html
<p [appHighlight]="'orange'">This has an orange background</p>
```

### Multiple Inputs Example

Directives can have multiple inputs, including the selector as an input:

```typescript
@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective implements OnInit {
  @Input("appHighlight") highlightColor = "yellow"; // Main color
  @Input() defaultColor = "transparent"; // Fallback color

  constructor(private el: ElementRef) {}

  ngOnInit() {
    this.el.nativeElement.style.backgroundColor =
      this.highlightColor || this.defaultColor;
  }
}
```

Usage:

```html
<p [appHighlight]="primaryColor" [defaultColor]="fallbackColor">
  Highlighted text
</p>
```

## Introducing `HostBinding` and `HostListener`

These are tools to interact with the host element (the element the directive is applied to) more elegantly than using `ElementRef`.

## @HostBinding in Detail

`@HostBinding` allows you to bind directive properties to properties of the host element. This is a more declarative approach than directly manipulating the DOM.

- **Purpose**: Binds a property of the host element (e.g., style, class) to a directive property.
- **Syntax**: `@HostBinding('property') variableName;`

### @HostBinding with a Simple Property

```typescript
@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective {
  @Input("appHighlight") highlightColor = "yellow";

  // Direct binding to a property
  @HostBinding("style.backgroundColor") backgroundColor: string;

  ngOnInit() {
    this.backgroundColor = this.highlightColor;
  }
}
```

> Note that background color will be changed once.

### @HostBinding with Getters for Dynamic Values

Getters are particularly useful when the binding value needs to be calculated:

```typescript
@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective {
  private _isActive = false;

  @Input("appHighlight") set active(value: boolean) {
    this._isActive = value;
  }

  // Bind to the class.active property using a getter
  @HostBinding("class.active") get isActive() {
    return this._isActive;
  }

  // Bind to style.backgroundColor with a calculated value
  @HostBinding("style.backgroundColor") get backgroundColor() {
    return this._isActive ? "yellow" : "transparent";
  }
}
```

Usage:

```html
<div [appHighlight]="isButtonActive">
  This div gets 'active' class when isButtonActive is true
</div>
```

### Common @HostBinding Properties

You can bind to various host element properties:

```typescript
@Directive({
  selector: "[appFeatures]",
})
export class FeaturesDirective {
  // CSS classes
  @HostBinding("class.special") isSpecial = true;

  // Styles
  @HostBinding("style.cursor") cursor = "pointer";

  // Attributes
  @HostBinding("attr.role") role = "button";

  // Properties
  @HostBinding("disabled") isDisabled = false;
}
```

## @HostListener in Detail

`@HostListener` allows directives to listen to events on the host element or on the global objects like `window` or `document`.

- **Purpose**: Listens to events on the host element (e.g., click, mouseover).
- **Syntax**: `@HostListener('eventName') method()`

### Basic @HostListener Usage

```typescript
import { Directive, ElementRef, HostListener } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective {
  constructor(private el: ElementRef) {}

  @HostListener("mouseenter") onMouseEnter() {
    this.el.nativeElement.style.backgroundColor = "yellow";
  }

  @HostListener("mouseleave") onMouseLeave() {
    this.el.nativeElement.style.backgroundColor = null;
  }
}
```

### @HostListener with Event Data

You can access event data using the `$event` parameter:

```typescript
@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective {
  constructor(private el: ElementRef) {}

  @HostListener("mouseenter", ["$event"]) onMouseEnter(event: MouseEvent) {
    console.log("Mouse position:", event.clientX, event.clientY);
    this.el.nativeElement.style.backgroundColor = "yellow";
  }
}
```

### @HostListener on Global Objects

You can listen to events on global objects like `window` or `document`:

```typescript
@Directive({
  selector: "[appTrackPosition]",
})
export class TrackPositionDirective {
  position = { x: 0, y: 0 };

  @HostListener("window:mousemove", ["$event"]) onMouseMove(event: MouseEvent) {
    this.position.x = event.clientX;
    this.position.y = event.clientY;
  }

  @HostListener("document:click", ["$event"]) onClick(event: MouseEvent) {
    console.log("Document clicked at:", event.clientX, event.clientY);
  }
}
```

### Using @HostListener with Control Flow

You can add conditions inside your event handlers:

```typescript
@Directive({
  selector: "[appContextMenu]",
})
export class ContextMenuDirective {
  @Input() appContextMenu = false; // Enable/disable context menu

  @HostListener("contextmenu", ["$event"]) onContextMenu(event: MouseEvent) {
    if (this.appContextMenu) {
      event.preventDefault(); // Prevent default browser context menu
      console.log("Custom context menu triggered");
      // Show your custom context menu
    }
  }
}
```

## Using Renderer2 for DOM Manipulation

While `ElementRef` gives direct access to DOM elements, it's better to use `Renderer2` for DOM manipulation.

`Renderer2` provides an abstraction layer that:

1. Is more secure (prevents XSS vulnerabilities)
1. Works with different rendering backends (like server-side rendering)
1. Makes testing easier

### Basic Renderer2 Usage

```typescript
import { Directive, ElementRef, Renderer2, OnInit } from "@angular/core";

@Directive({
  selector: "[appHighlight]",
})
export class HighlightDirective implements OnInit {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  ngOnInit() {
    // Instead of: this.el.nativeElement.style.backgroundColor = 'yellow';
    this.renderer.setStyle(this.el.nativeElement, "backgroundColor", "yellow");
  }
}
```

### Common Renderer2 Methods

```typescript
@Directive({
  selector: "[appFeatures]",
})
export class FeaturesDirective implements OnInit {
  constructor(private el: ElementRef, private renderer: Renderer2) {}

  ngOnInit() {
    // Setting styles
    this.renderer.setStyle(this.el.nativeElement, "fontSize", "16px");

    // Adding classes
    this.renderer.addClass(this.el.nativeElement, "highlighted");

    // Setting attributes
    this.renderer.setAttribute(
      this.el.nativeElement,
      "aria-label",
      "Interactive element"
    );

    // Setting properties
    this.renderer.setProperty(this.el.nativeElement, "disabled", true);

    // Adding event listeners
    this.renderer.listen(this.el.nativeElement, "click", () => {
      console.log("Element clicked!");
    });

    // Creating and appending elements
    const span = this.renderer.createElement("span");
    const text = this.renderer.createText("New content");
    this.renderer.appendChild(span, text);
    this.renderer.appendChild(this.el.nativeElement, span);
  }
}
```

## Practical Example 1: Custom Attribute Directive with `Renderer2`

Let’s create a directive that toggles a border on click.

### Code:

```typescript
import {
  Directive,
  Renderer2,
  ElementRef,
  HostListener,
  Input,
} from "@angular/core";

@Directive({
  selector: "[appBorderToggle]",
})
export class BorderToggleDirective {
  @Input() appBorderToggle = "2px solid black"; // Default border style
  private hasBorder = false;

  constructor(private renderer: Renderer2, private el: ElementRef) {}

  @HostListener("click") onClick() {
    this.hasBorder = !this.hasBorder;
    if (this.hasBorder) {
      this.renderer.setStyle(
        this.el.nativeElement,
        "border",
        this.appBorderToggle
      );
    } else {
      this.renderer.removeStyle(this.el.nativeElement, "border");
    }
  }
}
```

### Usage:

```html
<button appBorderToggle>Toggle my border!</button>
<button appBorderToggle="3px dashed blue">Toggle dashed border!</button>
```

- **Explanation**:
  - Clicking the button adds or removes a border.
  - `Renderer2`’s `setStyle` and `removeStyle` safely update the DOM.
  - The border style can be customized via the `@Input`.

## Practical Example 2: Building a Practical Custom Attribute Directive

Let's create a practical tooltip directive using everything we've learned:

```typescript
import {
  Directive,
  Input,
  ElementRef,
  Renderer2,
  HostListener,
} from "@angular/core";

@Directive({
  selector: "[appTooltip]",
})
export class TooltipDirective {
  @Input("appTooltip") tooltipText = "";
  @Input() tooltipPosition = "top"; // 'top', 'right', 'bottom', 'left'

  private tooltipElement: HTMLElement;

  constructor(private el: ElementRef, private renderer: Renderer2) {}

  @HostListener("mouseenter") onMouseEnter() {
    this.createTooltip();
  }

  @HostListener("mouseleave") onMouseLeave() {
    this.removeTooltip();
  }

  private createTooltip() {
    // Create tooltip element
    this.tooltipElement = this.renderer.createElement("div");
    this.renderer.addClass(this.tooltipElement, "tooltip");
    this.renderer.addClass(
      this.tooltipElement,
      `tooltip-${this.tooltipPosition}`
    );

    // Create text inside tooltip
    const text = this.renderer.createText(this.tooltipText);
    this.renderer.appendChild(this.tooltipElement, text);

    // Add tooltip to the body
    this.renderer.appendChild(document.body, this.tooltipElement);

    // Position the tooltip
    this.setPosition();
  }

  private setPosition() {
    const hostPos = this.el.nativeElement.getBoundingClientRect();
    const tooltipPos = this.tooltipElement.getBoundingClientRect();

    let top, left;

    switch (this.tooltipPosition) {
      case "top":
        top = hostPos.top - tooltipPos.height - 10;
        left = hostPos.left + (hostPos.width - tooltipPos.width) / 2;
        break;
      case "right":
        top = hostPos.top + (hostPos.height - tooltipPos.height) / 2;
        left = hostPos.right + 10;
        break;
      case "bottom":
        top = hostPos.bottom + 10;
        left = hostPos.left + (hostPos.width - tooltipPos.width) / 2;
        break;
      case "left":
        top = hostPos.top + (hostPos.height - tooltipPos.height) / 2;
        left = hostPos.left - tooltipPos.width - 10;
        break;
    }

    // Account for scrolling
    top += window.scrollY;
    left += window.scrollX;

    // Set position
    this.renderer.setStyle(this.tooltipElement, "top", `${top}px`);
    this.renderer.setStyle(this.tooltipElement, "left", `${left}px`);
  }

  private removeTooltip() {
    if (this.tooltipElement) {
      this.renderer.removeChild(document.body, this.tooltipElement);
      this.tooltipElement = null;
    }
  }
}
```

To use this directive, you'd need to add some CSS:

```css
/* In your global styles or component styles */
.tooltip {
  position: absolute;
  background-color: #333;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  z-index: 1000;
  font-size: 14px;
}

.tooltip::after {
  content: "";
  position: absolute;
  border-width: 5px;
  border-style: solid;
}

.tooltip-top::after {
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-color: #333 transparent transparent;
}

.tooltip-right::after {
  top: 50%;
  left: 0;
  margin-top: -5px;
  margin-left: -10px;
  border-color: transparent #333 transparent transparent;
}

.tooltip-bottom::after {
  bottom: 100%;
  left: 50%;
  margin-left: -5px;
  border-color: transparent transparent #333;
}

.tooltip-left::after {
  top: 50%;
  right: 0;
  margin-top: -5px;
  margin-right: -10px;
  border-color: transparent transparent transparent #333;
}
```

Usage in templates:

```html
<button [appTooltip]="'Click to submit'" tooltipPosition="top">Submit</button>
```

## Real-World Example: Click Outside Directive

This directive detects clicks outside of an element:

```typescript
import {
  Directive,
  ElementRef,
  EventEmitter,
  HostListener,
  Output,
} from "@angular/core";

@Directive({
  selector: "[appClickOutside]",
})
export class ClickOutsideDirective {
  @Output() appClickOutside = new EventEmitter<void>();

  constructor(private el: ElementRef) {}

  @HostListener("document:click", ["$event.target"]) onClick(target: any) {
    const clickedInside = this.el.nativeElement.contains(target);
    if (!clickedInside) {
      this.appClickOutside.emit();
    }
  }
}
```

Usage:

```html
<div class="dropdown" appClickOutside (appClickOutside)="closeDropdown()">
  <button (click)="toggleDropdown()">Toggle Dropdown</button>
  <div class="dropdown-menu" *ngIf="isOpen">
    <!-- Dropdown content -->
  </div>
</div>
```

These practical examples demonstrate the power and versatility of custom directives in Angular applications. They encapsulate reusable behaviors and can significantly improve your app's code organization and maintainability.

# TODO new syntax (trackby) - Importing ngClass in standalone

You can think of components as "directives with a view."

Component directives are the most common type of directive in Angular applications. A component combines a template, styles, and a TypeScript class to create a reusable piece of UI.

სარჩევი

custom structural directive
