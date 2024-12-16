# Angular-ის ლოკალურად დაყენება

## StackBlitz

თუ არ გსურთ ფაილებთან მუშაობა და ანგულარის ქომფაილერის დაყენება, შეგიძლიათ გამოიყენოთ ონლაინ [StackBlitz](https://stackblitz.com/) (ან მსგავსი პლატფორმა).

## ლოკალურად დაყენება

1. პირველ რიგში უნდა დავაყენოთ [Node.Js](https://nodejs.org/en) ოფიციალური ვებ გვერდიდან.

1. ასევე დაგვჭირდება ნებისმიერი კოდის ედიტორი, მაგალითად: [VS Code](https://code.visualstudio.com/).

1. Angular CLI-ის დაყენება

   გავხსნათ კონსოლი და ავკრიფოთ:

   ```
   npm install -g @angular/cli
   ```

   MacOS-ზე ან ლინუქსე:

   ```
   sudo npm install -g @angular/cli
   ```

   > `Node js` გვჭირდებოდა `npm` ბრძანების გამოსაყენებლად.

   > შეგვიძლია `install` შევამოკლოთ და დავწეროთ მხოლოდ `i`.

   > `-g`-ს ვუთითებთ `Angular CLI`-ის გლობალურად, ანუ მთლიან მოწყობილობაზე დასაყენებლად და არა კონკრეტულ დირექტორიაში.

   ### ვერსიის მითითება

   ```
   npm install -g @angular/cli
   ```

   > დააყენებს საბოლოო ვერსიას.

   ბოლოში `@`-ის დამატებით შეგვიძლია მივუთითოთ კონკრეტული ვერსია.

   ```
    npm install -g @angular/cli@16
   ```

# კომპონენტი

კომპონენტი წარმოადგენს ანგულარის ვებ-აპლიკაციის ძირითად სამშენებლო ბლოკს. ის წარმოადგენს `TypeScript`-ის კლასს, რომელიც აკონტროლებს ინტერფეისის ნაწილს.

სტრუქტურა:

- **Template**: განსაზღვრავს HTML სტრუქტურას.
- **Styles**: ანიჭებს სტილებს კომპონენტისთვის.
- **Class**: შეიცავს ბიზნეს ლოგიკასა და მონაცემებს კომპონენტისთვის.
- **Metadata**: შეიცავს კომპონენტის კონფიგურაციას (მაგ. სელექტორს, Template-ს, სტილებს).

## კომპონენტის შექმნა

```
ng generate component component-name
```

ან შემოკლებული ფორმა

```
ng g c component-name
```

---

### კომპონენტი Inline ტემპლეიტით

```
ng generate component component-name --inline-template
```

ან შემოკლებული

```
ng g c component-name --it
```

---

### კომპონენტი Inline სტილებით

```
ng generate component component-name --inline-style
```

ან შემოკლებული

```
ng g c component-name --is
```

---

### კომპონენტი Inline სტილებითა და ტემპლეიტით

```
ng generate component component-name --inline-template --inline-style
```

ან შემოკლებული

```
ng g c component-name --it --is
```

---

### კომპონენტი სტილების გარეშე

```
ng generate component component-name --style none
```

---

### კომპონენტი ტესტირების ფაილის გარეშე

```
ng generate component component-name --skip-tests
```

ან შემოკლებული

```
ng g c component-name --st
```

# Data Binding

`Data binding` ერთმანეთთან აკავშირებს `User Interface`-სა (HTML ფაილსა) და `მოდელს` (ტაიპსკრიპტის ფაილს). უფრო მარტივი სიტყვებით, მისი საშუალებით შეგვიძლია გადავცეთ ან შევცვალოთ ცვლადების მნიშვნელობები კომპონენტის კლასიდან მის HTML ფაილში, ან პირიქით.

**უფრო მეტიც, ეს კავშირი სინქრონიზებულია.**

ამიტომ ცვლადის შეცვლისას მისი ახალი მნიშვნელობა მაშინვე აისახება ვებ-გვერდზე. შესაბამისად, არ გვიწევს ზედმეტი და კომპლექსური ლოგიკის გაწერა თითოეული მოვლენის აღმოსაჩენად, რაც გვიმარტივებს კოდის წერას და ამით მცირდება შეცდომის დაშვების ალბათობაც.

ანგულარი ამ ყველაფერს აღწევს `Change Detection Cycle`-ის გამოყენებით.

## Data Binding-ის ტიპები

ანგულარი გვთავაზობს ორი ტიპის `data binding`-ს:

- `One-way`, ანუ ერთ და
- `Two-way` - ორმხრივს data binding-ს.

### One-Way Data Binding

**One-way data binding-ში მონაცემები გადაეცემიან მხოლოდ ერთი მიმართულებით.**

ამიტომ ის შეგვიძლია დავყოთ ორ ტიპად:

1. **Component to view**, რომელშიც მონაცემები გადაეცემიან კომპონენტის კლასიდან მის View template-ში. ასეთებია: `String Interpolation`, `Property` და `Attribute` binding.

1. და პირიქით, **View to component**, როდესაც მოხმარებელი, User Interface-ით ცვლის კლასის ცვლადებს. ასეთია `Event binding`.

### Two-Way Data Binding

**Two-way data binding-ში კი მონაცემები გადაეცემიან ორივე მიმართულებით ერთდროულად.**

## One-way Data Binding

### `String Interpolation`

ვთქვათ, კომპონენტის კლასში მოცემული გვაქვს ტემპერატურის ცვლადი, რომელიც დინამიურია და შეიცვლება:

```TS
temperature: number = 23;
```

ჩვენ ვაპირებთ ამ ცვლადის html-ში ასახვას.

ამისთვის დაგვჭირდება `One-Way Data Bidning`, კერძოდ, `String Interpolation`.

გადავიდეთ `HTML`-ში და უბრალოდ ჩავწეროთ ორი ფიგურული ფრჩხილის წყვილი - `{{}}` და შიგნით მივუთითოთ ჩვენი ცვლადის სახელი.

```HTML
<p> The temperature is {{ temperature }} degrees Celsius. </p>
```

---

მხოლოდ ცვლადის გამოტანით არ ვიფარგლებით.

`String Interpolation`-ში იწერება ვალიდური `JavaScripct.`

`app.component.html`:

```HTML
<p> The temperature is {{ temperature * 2 }} degrees Celsius. </p>
```

```HTML
<p> The temperature is {{ temperature * 2 }} degrees Celsius. </p>
```

```HTML
<p> The temperature is {{ 10 + 20 }} degrees Celsius. </p>
```

```HTML
<p> My name is {{ ('John' + ' ' + 'Doe').toUpperCase() }}. </p>
```

```HTML
<p> {{ temperature < 0 ? "Cold" : "Warm" }} </p>
```

ასევე შეგვიძლია მივუთითოთ ფუნქცია, რომელიც გვიბრუნებს რაიმე მნიშვნელობას:

`app.component.ts`:

```TS
calculateSum(): number{
    return 10 + 20
}
```

`app.component.html`:

```HTML
<p> Sum is {{ calculateSum() }} </p>
```

> დავიმახსოვროთ, რომ `String Interpolation`-ში არ შეგვიძლია:
>
> - ახალი ცვლადის შექმნა ან მინიჭევა (=, +=, -=, ...);
> - `new`, `typeof`, ან `instanceof` ოპერატორების გამოყენება;
> - Chaining expressions with `;` or `,`. მაგალითად: `<p>{{  20 + 10; temperature  }}</p>` ან `<p>{{  20 + 10, temperature  }}</p>`
> - ინკრემენტაციის (++) და დეკრემენტაციის ოპერაციების გამოყენება (--). მაგალიტად: `<p>{{  temperature++  }}</p>`

### `Property Binding`

თუ ვაპირებთ დინამიურად შევცვალოთ ელემენტის პარამეტრი / თვისება, მაშინ უნდა გამოვიყენოთ `Property Binding`. ამისთვის, თვისება ან უნდა ჩავსვათ კვადრატულ ფრჩხილებში `[]`, ან წინ მივუწეროთ `bind`, თუმცა `[]` უფრო ხშირად გვხვდება.

`app.component.ts`:

```TS
quantity: number = 10
```

`app.component.html`:

```HTML
<button type="button" [disabled]="quantity === 0">Buy Now</button>
```

ან

```HTML
<button type="button" bind-disabled="quantity === 0">Buy Now</button>
```

> `String Interpolation` გვიბრუნდებს `string`-ს, ამიტომ ის არ იმუშავებს ყველა პარამეტრთან, მაგალითად: `Disabled`, `Checked`, `Hidden`, რადგან ისინი ელოდებიან `Boolean`-ის მნიშვნელობას და არა სტრინგს. ამიტომ უკეთესი იქნება, თუ პარამეტრთან ყოველთვის გამოვიყენებთ მხოლოდ `Property Binding`-ს.

#### ბონუს კონტენტი

ანგულარში ელემენტის კლასისა თუ სტილის შეცვლა შესაძლებელია ორი მეთოდით. პირველს განვიხილავთ `Directive`-ების ლექციაზე. ხოლო მეორე შესაძლებელია სწორედ `Property Binding`-ით.

##### კლასების დინამიურად შეცვლა

`app.component.ts`:

```TS
isActive = true;
```

`app.component.html`:

```HTML
<div [class.active]="isActive" [class.disabled]="!isActive"> Some Information </div>
```

---

##### სტილების დინამიურად შეცვლა

`app.component.ts`:

```TS
bgColor = 'blue';
fontSize = 20;
```

`app.component.html`:

```HTML
<div [style.background-color]="bgColor" [style.font-size.px]="fontSize"> Some Information </div>
```

### `Attribute Binding`

Attribute Binding-ის საშუალებით შეგვიძლია დინამიურად ვცვალოთ ელემენტის Attribute-ები.

`app.component.ts`:

```TS
buttonLabel = 'Submit button';
```

`app.component.html`:

```HTML
<button [attr.aria-label]="buttonLabel">Submit</button>
```

### `Event Binding`

გარჩეული binding-ების ტიპებიდან განსხვავებით, `Event binding`-ის საშუალებით, მომხმარებელს `User Interface`-თან ურთიერთქმედებით შეუძლია შეცვალოს კომპონენტის კლასის ცვლადების მნიშვნელობები.

სხვა სიტყვებით, მონაცემები `View template`-დან `კლასში` გადაეცემიან.

ნებისმიერ მოვლენაზე (Event-ზე) შეგვიძლია მივუთითოთ რაიმე ფუნქცია. მაგალითად, ღილაკის დაჭერაზე, ტექსტის აკრეფვაზე და ასე შემდეგ.

`app.component.ts`:

```TS
showMessage() {
    console.log('Hello Angular!');
}
```

`app.component.html`:

```HTML
<button (click)="showMessage()">Click me</button>
```

```HTML
<div (mouseover)="showMessage()">Hover Over me</div>
```

---

`app.component.ts`:

```TS
onInputChange(event: Event) {
    const inputElement = event.target as HTMLInputElement;
    console.log('Input value:', inputElement.value);
}
```

`app.component.html`:

```HTML
<input (input)="onInputChange($event)" placeholder="Type something">
```

> `$event` აკრეფვაზე შესრულებული event-ია.

ბრჭყალებში არა მარტო ფუნქციის მითითება შეგვიძლია, არამედ ჯავასკრიპტის კოდის ჩაწერაც.

სტრინგის ინტერპოლაციასთან განსხვავებით, აქ შეგვიძლია ცვლადების გაზრდა, მათთვის მნიშვნელობების შეცვლა და მრავალი სხვა.

> თუმცა, ჩვენ არ შეგვიძლია მივმართოთ დოკუმენტს, ან მთლიან ფანჯარას, ამიტომ აქ ვერ დავწერთ `console.log`-ს. ვერც გამოვიყენებთ `Math.max()`-ს.

#### სხვა event-ები რომელთა მოსმენა შეგვიძლია

##### 1. Mouse Events

- `(click)` — ელემენტზე დაწკაპუნება.
- `(dblclick)` — ელემენტზე ორმაგი დაწკაპუნება.
- `(mousedown)` — ელემენტზე დაწკაპუნება.
- `(mouseup)` — მოუსის ღილაკის გაშვება.
- `(mouseenter)` — მაუსის მაჩვენებლის შესვლა ელემენტზე.
- `(mouseleave)` — მაუსის მაჩვენებლის გამოსვლა ელემენტიდან.
- `(mousemove)` — მაუსის მოძრაობა ელემენტზე.
- `(mouseover)` — მაუსის მაჩვენებლის გადაადგილება ელემენტზე და მის შვილებზე.
- `(mouseout)` — მაუსის მაჩვენებლის გამოსვლა ელემენტიდან და მისი შვილებიდან.

##### 2. Keyboard Events

- `(keydown)` — კლავიატურის ღილაკის დაჭერა.
- `(keypress)` — კლავიატურის ღილაკის დაჭერა და აშვება (მოძველებულია Angular-ის ახალ ვერსიებში).
- `(keyup)` — კლავიატურის ღილაკის აშვება.
- `(input)` — `<input>`, `<textarea>`, ან `<select>` მონაცემების შეყვანა.

##### 3. Focus Events

- `(focus)` — ელემენტზე ფოკუსირება.
- `(blur)` — ფოკუსის დაკარგვა.

##### 4. Form Events

- `(change)` — Form-ის ელემენტების მნიშვნელობის ცვლილება.
- `(submit)` — Form-ის გაგზავნა.
- `(reset)` — Form-ის დარესეტება.

> `input` vs `change` - `input` იშვება ყოველი აკრიფვისას, `change` კი აკრიფვისას და blur event-ის შესრულებისას (ფოკუსის დაკარგვისას).

##### 5. Touch Events

- `(touchstart)` — ეკრანზე შეხების დაწყება.
- `(touchend)` — ეკრანზე შეხების დასრულება.
- `(touchmove)` — მაგ: ეკრანზე თითის გადატარება.
- `(touchcancel)` — ეკრანზე შეხების შეწყვეტა.

##### 6. Drag Events

- `(drag)` — ელემენტის გადაადგილება.
- `(dragstart)` — ელემენტის გადაადგილების დაწყება.
- `(dragend)` — ელემენტის გადაადგილების დასრულება.
- `(dragover)` — ელემენტის გადაადგილება გაშვების ზონაზე.
- `(dragenter)` — ელემენტის შესვლა გაშვების ზონაში.
- `(dragleave)` — ელემენტის გამოსვლა გაშვების ზონიდან.
- `(drop)` — ელემენტის გაშვება.

## Two-Way Data Binding

`Two-Way Data Binding`-Si მონაცემები ორივე მიმართულებით ერთდროულად გადაეცემიან.

ანუ მომხმარებელს შეუძლია `User Interface`-თან ურთიერთქმედებით, კერძოდ `Event binding`-ით შეცვალოს კომპონენტის კლასის მონაცემები და ამავდროულად კლასიდან `String Interpolation`, `Property`, `Attribute` და `Event binding`-ით შეცვალოს HTML.

> გამოდის, რომ `Two-Way Data Binding` არის `Property` და `Event Binding`-ების კომბინაცია.

ამისთვის დაგვჭირდება `FormsModule`.

- თუ მუშაობთ ანგულარის მე-17 ან უფრო ახალ ვერსიაზე, ანუ გაქვთ **Standalone** კომპონენტები, `FormsModule` პირდაპირ კომპონენტის იმპორტებში შემოიტანეთ.

  `app.component.ts`:

  ```TS
  import { Component } from '@angular/core';
  import { FormsModule } from '@angular/forms';

  @Component({
    selector: 'app-standalone-form',
    standalone: true,
    imports: [FormsModule], // <--
    template: ``
  })
  export class StandaloneFormComponent {
    username: string = '';
  }
  ```

- ხოლო თუ მუშაობთ **Non-Standalone** კომპონენტებთან, გადადით `NgModule`-ში და დაამატეთ მთლიანი აპლიკაციისთვის.

  `app.module.ts`:

  ```TS
  import { NgModule } from '@angular/core';
  import { BrowserModule } from '@angular/platform-browser';
  import { FormsModule } from '@angular/forms';

  import { AppComponent } from './app.component';

  @NgModule({
  declarations: [
      AppComponent
  ],
  imports: [
      BrowserModule,
      FormsModule  // <--
  ],
  providers: [],
  bootstrap: [AppComponent]
  })
  export class AppModule { }
  ```

ახლა შეგვიძლია `ngModel` დირექტივის გამოყენება.

მისი სინტაქსი შემდეგნაირია: `[()]` და შიგნით ვწერთ `ngModel`-ს.

> `Two-Way Data Binding` არის `Property` - `[]` და `Event binding`-ის - `()` კომბინაცია. აქედან ვიღებთ `[()]`.
>
> მარტივად დასამახსოვრებლად, თვითონ ანგულარის დომუკენტაციაშიც იხილავთ, რომ ამ სინტაქსს მიმართავენ როგორც `ბანანს ყუთში`.

`app.component.ts`:

```TS
name: string = '';
```

`app.component.html`:

```HTML
<label for="name">Enter your name:</label>
<input id="name" [(ngModel)]="name" placeholder="Enter name">

<p>Your name is: {{ name }}</p>
```

ასევე გვაქვს მეორე სინტაქსი. ცალ-ცალკე `property` და `event binding`-ები:

```HTML
<label for="name">Enter your name:</label>
<input id="name" [ngModel]="name" (ngModelChange)="name = $event" placeholder="Enter name">
<input >
```

> რეალურად, ეს ორი სინტაქსი ერთი დ იგივეს აკეთებს, ამიტომ უკანასკნელს იშვიათად ვიყენებთ.

# შეჯამება

| ტიპი                 | სინტაქსი                                                 | აღწერა                                           | მაგალითი                                              |
| -------------------- | -------------------------------------------------------- | ------------------------------------------------ | ----------------------------------------------------- |
| String Interpolation | `{{ expression }} `                                      | გამოსახავს კომპონენტის ცვლადს ტემპლეიტში         | `<p>{{ name }}</p>`                                   |
| Property Binding     | `[property]="expression"` / `bind-property="expression"` | დინამიურად ცვლის ელემენტის თვისებებს             | `<img [src]="imageUrl">`                              |
| Attribute Binding    | `[attr.attributeName]="expression"`                      | დინამიურად ცვლის ელემენტის ატრიბუტებს            | `<button [attr.aria-label]="label">Click Me</button>` |
| Event Binding        | `(event)="method()"`                                     | უსმენს სხვადასხვა event-ებს და იძახებს ფუნქციებს | `<button (click)="onClick()">Click Me</button>`       |
| Two-Way Binding      | `[(ngModel)]="property"`                                 | სინქრონულად აკავშირებს ტემპლეიტსა და მოდელს      | `<input [(ngModel)]="name">`                          |
|                      |

# მონაცემების გაცვლა კომპონენტებს შორის

## Parent to Child - Custom Property Binding

1.  აუცილებლად უნდა გვქონდეს მშობელი და შვილი კომპონენტები.
1.  გადავიდეთ `child.component.ts`-ში და შევქმნათ ცვლადი, რომელშიც შევინახავთ მშობლიდან მიღებულ მონაცემებს:

    ```TS
    import { Component, Input } from '@angular/core';

    @Component({
    selector: 'app-child',
    template: `  <p>The input value is: {{ childProperty }}</p>`
    })
    export class ChildComponent {
        @Input() childProperty: string = ''; // ან მიეცით საწყისი მნიშვნელობა

        // ან

        @Input() childProperty!: string;
    }
    ```

1.  გადადით მშობელში და `child` კომპონენტზე გამოიყენეთ `Custom Property Binding` - `[]`. ფრჩხილებში მოათავსეთ შვილის იმ ცვლადის სახელი, რომელსაც ანიჭებთ მნიშვნელობას.`parent.component.ts`:

    ```TS
    import { Component } from '@angular/core';

    @Component({
        selector: 'app-parent',
        template: `
            <app-child [childProperty]="parentProperty" />
        `,
        imports: [ChildComponent]
    })
    export class ParentComponent {
        parentProperty: string = 'Hello from Parent!';
    }
    ```

### Alias

თუ არ მოგწონთ `@Input` ცვლადის სახელი, Custom Property Binding-ში შეგვიძლია მივუთითოთ ალტერნატიული სახელი.

`child.component.ts`:

```TS
import { Component, Input } from '@angular/core';

@Component({
    selector: 'app-child',
    template: `<p>The input value is: {{ childProperty }}</p>`
})
export class ChildComponent {
    @Input('customName') childProperty: string = ''; // Alias
}
```

`parent.component.ts`:

```TS
import { Component } from '@angular/core';

@Component({
    selector: 'app-parent',
    template: `
        <app-child [customName]="parentProperty" />
    `,
    imports: [ChildComponent]
})
export class ParentComponent {
    parentProperty: string = 'Hello from Parent!';
}
```

## Child to Parent - Custom Event Binding

აქ პირიქით, მოცანემებს ვაგზავნით შვილიდან მშობელში.

1.  შვილ კომპონენტში განსაზღვრეთ `@Output()` დეკორატორი ცვლადზე `EventEmitter`-ის გამოყენებით.

    `child.parent.ts`:

    ```TS
    import { Component, Output, EventEmitter } from '@angular/core';

    @Component({
        selector: 'app-child',
        template: `<button (click)="sendMessage()">Send Message</button>
    `
    })
    export class ChildComponent {
        @Output() customEvent = new EventEmitter<string>(); // EventEmitter მონაცემების გამოსაყოფად

        sendMessage() {
            this.customEvent.emit('Hello from Child!');
        }
    }
    ```

1.  დააკავშირეთ მოვლენა (`event`) მშობელ კომპონენტში ფრჩხილების გამოყენებით `()`.

    `parent.component.ts`:

    ```TS
    import { Component } from '@angular/core';

    @Component({
        selector: 'app-parent',
        template: `<app-child (customEvent)="receiveMessage($event)" />  <!-- Custom event binding -->
            <p>{{ message }}</p> <!-- $event არის გადაცემული მონაცემი-->
        `
    })
    export class ParentComponent {
        message: string = '';

        receiveMessage(eventData: string) {
            this.message = eventData; // მონაცემების მიღება
        }
    }
    ```

## Nonrelated - Sibling Components

გეგმა:

1. **Custom Event Binding**-ით გადავცეთ მონაცემები `Child1`-დან `Parent`-ში.
1. `Parent`-დან **Custom Property Binding**-ით გადავცეთ `Child2`-ში.

`child1.component.ts`:

```TS
import { Component, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child1',
  template: `<button (click)="sendMessage()">Send Message to Child 2</button>`
})
export class Child1Component {
  @Output() sendMessage = new EventEmitter<string>();

  sendMessage() {
    this.sendMessage.emit('Hello from Child 1');
  }
}
```

`parent.component.ts`:

```TS
import { Component } from '@angular/core';

@Component({
  selector: 'app-parent',
  template: `
    <app-child1 (sendMessage)="receiveMessage($event)"></app-child1>
    <app-child2 [message]="message"></app-child2>
  `
})
export class ParentComponent {
  message: string = '';

  receiveMessage(eventData: string) {
    this.message = eventData;
  }
}
```

`child2.component.ts`:

```TS
import { Component, Input } from '@angular/core';

@Component({
  selector: 'app-child2',
  template: `<p>Received Message: {{ message }}</p>`
})
export class Child2Component {
  @Input() message: string = '';
}
```
