# რა არის TypeScript?

`TypeScript` არის JavaScript-ის გაუმჯობესებული ვერსია, დამატებითი ფუნქციონალით.

ის იყენებს იგივე სინტაქსს, რაც `JavaScript`, ანუ ნებისმიერი `JavaScript`-ის კოდი ვალიდარუი `TypeScript`-ია. თუმცა, აქ ასევე შემოღებულია **სტატიკური ტიპები და უფრო მკაცრი წესები,** რათა დეველოპერმა შეძლოს კოდში დაშვებული შეცდომის აღმოჩენა კომპილაციის დროს და არა კოდის გაშვებისას. ეს არის ერთ-ერთი მიზეზი, რის გამოც `TypeScript` გამოიყენება დიდი აპლიკაციების შემუშავებაში და სწორედ ამიტომაც `Angular` იყენებს მას.

# TypeScript-თან მუშაობა

სტანდარტულად ბრაუზერს არ შეუძლია TypeScript-ის კოდის წაკითხვა, რის გამოც გვიწევს კოდის JavaScript-ზე გადაყვანა.

## Online Playground

თუმცა, თუ არ გსურთ ფაილებთან მუშაობა და ტაიპსკრიპტის ქომფაილერის დაყენება, შეგიძლიათ გამოიყენოთ ონლაინ ქომფაილერი. საბედნიეროდ, ასეთი ბევრია.

- [ოფიციალური TypeScript-ის Playground](https://www.typescriptlang.org/play/?#code/PTAEHUFMBsGMHsC2lQBd5oBYoCoE8AHSAZVgCcBLA1UABWgEM8BzM+AVwDsATAGiwoBnUENANQAd0gAjQRVSQAUCEmYKsTKGYUAbpGF4OY0BoadYKdJMoL+gzAzIoz3UNEiPOofEVKVqAHSKymAAmkYI7NCuqGqcANag8ABmIjQUXrFOKBJMggBcISGgoAC0oACCbvCwDKgU8JkY7p7ehCTkVDQS2E6gnPCxGcwmZqDSTgzxxWWVoASMFmgYkAAeRJTInN3ymj4d-jSCeNsMq-wuoPaOltigAKoASgAywhK7SbGQZIIz5VWCFzSeCrZagNYbChbHaxUDcCjJZLfSDbExIAgUdxkUBIursJzCFJtXydajBBCcQQ0MwAUVWDEQC0gADVHBQGNJ3KAALygABEAAkYNAMOB4GRonzFBTBPB3AERcwABS0+mM9ysygc9wASmCKhwzQ8ZC8iHFzmB7BoXzcZmY7AYzEg-Fg0HUiQ58D0Ii8fLpDKZgj5SWxfPADlQAHJhAA5SASPlBFQAeS+ZHegmdWkgR1QjgUrmkeFATjNOmGWH0KAQiGhwkuNok4uiIgMHGxCyYrA4PCCJSAA)
- [StackBlitz](https://stackblitz.com/)

> აქ დაყენების გარეშე, პირდაპირ შეგვიძლია დავიწყოთ კოდის წერა.

## ლოკალურად დაყენება

1. პირველ რიგში უნდა დავაყენოთ [Node.Js](https://nodejs.org/en) ოფიციალური ვებ გვერდიდან.

1. ასევე დაგვჭირდება ნებისმიერი კოდის ედიტორი, მაგალითად: [VS Code](https://code.visualstudio.com/).

1. ტაიპსკრიპტის ქომფაილერის დაყენება

   გავხსნათ კონსოლი და ავკრიფოთ:

   ```
   npm install -g typescript
   ```

   MacOS-ზე ან ლინუქსე:

   ```
   sudo npm install -g typescript
   ```

   > `Node js` გვჭირდებოდა `npm` ბრძანების გამოსაყენებლად.

   > შეგვიძლია `install` შევამოკლოთ და დავწეროთ მხოლოდ `i`.

   > `-g` ვუთითებთ `TypeScript`-ის ქომფაილერის გლობალურად, ანუ მთლიან მოწყობილობაზე დასაყენებლად და არა კონკრეტულ დირექტორიაში.

1. დაყენების დასრულების შემდეგ აკრიფეთ

   ```
   tcs -v
   ```

   > `tcs` ნიშნავს ტაიპსკრიპტის ქომფაილერის

   > `-v` ვერსიას.

   ამის შემდეგ შექმენით ჯერ `index.html` ფაილი.

   შემდეგ კი ტაიპსკრიპტის ფაილი და დავარქვით `main.js`.

   როგორც ვახსენე, ტაიპსკრიპტი დაფუძნებულია ჯავასკრიპტზე, ამიტომ აქ შეგვიძლია ჩავწეროთ ჯავასკრიპტის კოდი.

   ```TS
   const name = “John”

   console.log(name)
   ```

   რადგან ბრაუზერი ვერ ხედავს ტაიპსკრიპტის კოდს, გადავიდეთ ტერმინალში, დავრწმუნდეთ რომ სწორ საქაღალდეში ვდგავართ და ჩავწეროთ:

   ```
   tsc main.ts
   ```

   ანუ ჩვენ გვსურს გადავიყვანოთ `main.ts` ფაილი `main.js`-ად.

   > ყოველი ცვლილების შემდეგ თავიდან მოგვიწევს ამ ბრძანების აკრეფა, რაც კომფორტული არაა.

   ამიტომ ამ ბრძანებას ბოლოს დავუმატოთ `-w`, რაც ნიშნავს watch-ს, ყურებას. ასე რომ ყოველი შენახვისას ავტომატურად გაიშვება ეს ბრძანდება და მოხდება ტაიპსკრიპტის კონვერტაცია.

   ```
   tsc main.ts -w
   ```

   საბოლოოდ HTML მივუთითოთ JS-ს ფაილი:

   ```HTML
    <script src="main.js" defer></script>
   ```

# Basic Static Types

`JavaScript` არის **Dynamically Typed** - აქ ცვლადის ტიპი დინამიურია. ამიტომ ერთხელ გამოცხადებული სტრინგის ცვლადს შეგვიძლია მივანიჭოთ რიცხვითი მნიშვნელობა ან სხვა.

`TypeScript` კი არუს **Statically Typed** - თუ ჩვენ გამოვაცხადებთ რაიმე ცვლადს და ვიტყვით რომ ის სტრინგია, ვერ შევძლებთ მის სხვა ტიპზე შეცვლას.

## Type Number

ტიპის მითითება შეგვიძლია ცვლადის სახელის მერე, `:`-ის გამოყენებით

```TS
let age: number = 30;
```

სხვა სტატიკურ ენებისგან განსხვავებით ტაისპკრიპტში მთელი რიცხვები, ანუ int და ათწილადები: float ან double, ერთმანეთისგან არ არიან გამოყოფილნი, რადგან number მოიცავს ყველა მათგანს.

შესაბამისად:

```TS
let num: number = 30.5
```

> თუ მივანიჭებთ რაიმე სტრინგის მნიშვნელობას, დავინახავთ შეცდომას.

## Type String

ეს არის ისეთი ტიპი, რომელიც ინახავს ტექსტურ მნიშვნელობას.

```TS
let message: string = "Hello World!";
```

## Type Boolean

```TS
let isEditing: boolean = false;
```

## Explicit vs Implicit Type Declaration

თუ ვმუშაობთ მარტივ ტიპებთან და მომავალში არ ვაპირებთ მათი ტიპის შეცვლას, მაშინ შეგვიძლია გამოვტოვოთ ტიპის მითითება და ტაიპსკრიპტის კომპაილერი თვითონ გამოიცნობს ცვლადის ტიპი მისი, **მნიშვნელობის მიხედვით**.

```TS
let age_imp = 30 // Implicit Type Declaration
let age_exp: number = 30 // Explicit Type Declaration
```

> თუ კურსორს გადავატარებთ age-ზე, ვნახავთ რომ მის ტიპი number-ია.

## Type Any

თუ არ გვსურს ტიპებზე ფიქრი და გვინდა ისეთი ცვლადის შექმნა, რომელსაც მივანიჭებთ ნებისმიერ ტიპს, გამოიყენეთ `any`. `Any` ყველაფრის ნებას მოგვცემს. ასეთ ცვლადს ყველაფერი შეგვიძლია მივანიჭოთ. `Any`-ს მაშინ ვიყენებთ, როცა API-დან ველოდებით რაიმე respone-ს და არ ვიცით თუ რას დაგვიბრუნებს.

> თუმცა, მისი გამოყენებით იკარგება ტაიპსკრიპტის გამოყენების აზრი, რადგან კომფაილერი ვერ შეძლებს შეცდომის აღმოჩენას. ამიტომ აერიდეთ მის გამოყენებას.

```TS
let x: any = true;

x++;
x.toUpperCase();
x.name;
x();
```

## Type Unknown

თუ მაინც გვსურთ ყველა ტიპთან მუშაობა, უკეთესი იქნება თუ გამოვიყენებთ მეორე ტიპს რომელსაც ამატებს ტაიპსკრიპტი - `Unknown`. ის any-ს მსგავსია, თუმცა უფრო დაცული. თუ ცვლადს მივანიჭებთ ამ ტიპს, ნებისმიერ ქმედებაზე გვექნება შეცდომა. პირველ რიგში უნდა შევამოწმოთ თუ რა ტიპთან ვმუშაობთ. მაგალითად, თუ დარწმუნებულები ვართ რომ ჩვენი ცვლადი რიცხვია, მხოლოდ მაშინ შეგვძელება როცხვებთან დაკავშირებული ნებისმიერი ოპერაციის შესრულება, სტრინგთან სტრინგების და ასე შემდეგ. ასეთ მეთოდს ჰქვია `type narrowing`.

```TS
let y: unknown = true;

if (typeof y === 'number') { // Type Narrowing
  y++;
}
if (typeof y === 'string') {
  y.toUpperCase();
}
```

# Array

მასივის შექმნა:

```TS
const num_arr: number[] = [1, 2, 3, 4, 5];
```

ან

```TS
const str_arr: Array<string> = ['a', 'b', 'c', 'd', 'e'];
```

> ორივე სინტაქსი მიღებულია.

თუ ინიციალიზაციისას შევიტანთ მხოლოდ სტრინგებს, მაშინ ტაიპსკრიპტი ჩათვლის, რომ ამ მასივში მხოლოდ სტრინგები უნდა შევინახოთ და ფიქსირებულ ტიპს მისცემს.

```TS
const arr = ['a', 'b', 'c', 'd', 'e'] // Implicit Declaration - string[]
```

# Union

თუ ცვლადზე გვინდა რამდენიმე ტიპის მითითება, მაგალითად `string`-სა ან `number`-ის, `any` ან `unknown`-ის ნაცვლად უკეტესი იქნება თუ გამოვიყენებთ `Union`-ს, ამისთვის დავწეროთ ბიტური ოპერატორი 'ან' - `|`.

```TS
let ageOrNum: number | string = 'John'
```

> შეეცადეთ არ გადატვირთოთ ტიპებით.

```TS
const arr: (string | number)[] = [1, 'a', 2, 'b']
const arr1: Array<string | number> = [1, 'a', 2, 'b']
```

# ფუნქციები

ფუნქციის პარამეტრებს უნდა მივუთითოთ ტიპები:

```TS
function sum(a: number, b: number){
    return a + b;
}
```

ფუნქციის მნიშვნელობა შევინახოთ რაიმე ცვლადში.

```TS
const result = sum(10, 20)
```

რადგან ფუნქცია აბრუნებს რიცხვს, `result`-იც იქნება რიცხვი.

```TS
function sum(a: number, b: number): number{
    return a + b;
}

const result: number = sum(10, 20)
```

ზუსტად იგივე პრინციპით მუშაობს `arrow function`-იც.

```TS
let sum = (a: number, b: number): number => {
    return a + b
}
```

თუ ფუნქცია არაფერს არ აბრუნებს, მაშინ `return type`-ად მიუთითეთ: `void`

```TS
function sum(a: number, b: number): void{
    console.log(a + b)
}
```

> ტიპების მიწერა კარგი პრაქტიკაა,

## Optional Parameter

ეს ისეთი პარამეტრია, რომელიც შეგვიძლია არ მივაწოდოთ. ამისთვის გამოცხადებისას ტიპთან მივუთითოთ **კითხვის ნიშანი**.

```TS
function sum(a: number, b?: number): number{
    if(b){
        return a + b
    }

    return a + a
}
```

## Default Parameter

ის როგორც არასავალდებულო პარამეტრია, თუმცა ინახავს საწყის მნიშვნელობას, იმ შემთხვევაში, თუ ჩვენ არაფერს არ გადავცემთ.

```TS
function sum(a: number, b: number = 10): number{
    return a + b
}
```

> Default და არასავალდებულო პარამეტრები აუცილებლად უნდა იყონ ბოლოში და არა ფუნქციის თავში.

# OOP

კლასების შესწავლა ძალზედ მნიშვნელოვანია, რადგან ანგულარის კომპონენტის მოდელი სწორად ტაიპსკრიპტის კლასს წარმოადგენს.

კლასის შექმნის პროცესი იგივეა რაც ჯავასკრიპტში:

```TS
class Person {
  id: string;
  name: string;
  age: number;

  constructor(id: string, name: string, age: number) {
    this.id = id;
    this.name = name;
    this.age = age;
  }

  information() {
    console.log('Id: ' + this.id, 'Name: ' + this.name, 'Age: ' + this.age);
  }
}

const person1_class = new Person('111', 'George', 20);
```

## Access Modifiers

TypeScript-ში წვდომის მოდიფიკატორები აკონტროლებენ კლასის წევრების ხილვადობას. ისინი განსაზღვრავენ, თუ როგორ და სად შეიძლება წევრზე წვდომა თქვენი პროგრამის ფარგლებში.

TypeScript-ში სამი ძირითადი წვდომის მოდიფიკატორია:

- `public` (Default)
- `private`
- `protected`

### 1. Public

წევრი, რომელიც მონიშნულია `public`-ად, ხელმისაწვდომია ნებისმიერი ადგილიდან, როგორც კლასის შიგნით, ასევე მის ფარგლებს გარეთ.

თუ წვდომის მოდიფიკატორი არ არის მითითებული, `TypeScript` მას `public` ხდის.

```TS
class Car {
  public brand: string;

  constructor(brand: string) {
    this.brand = brand;
  }

  public displayBrand() {
    console.log(`The car brand is ${this.brand}`);
  }
}

const car = new Car("Tesla");
console.log(car.brand);   // ხელმისაწვდომია კლასის გარეთ
car.displayBrand();       // ხელმისაწვდომია კლასის გარეთ
```

### 2. Private

წევრები, რომლებიც მონიშნულია როგორც `private`, ხელმისაწვდომი არიან მხოლოდ კლასში. მათ ვერ მივწვდებით კლასის გარედან.

ეს გვეხმარება მნიშვნელოვანი და სენსეტიური მონაცემების დასამალად.

```TS
class Car {
  private model: string;

  constructor(model: string) {
    this.model = model;
  }

  public displayModel() {
    console.log(`The car model is ${this.model}`);
  }
}

const car = new Car("Model X");
console.log(car.model);  // Error: Property 'model' is private and only accessible within class 'Car'.
car.displayModel();
```

### 3. Protected

`Protected` წევრები ხელმისაწვდომნი არიან კლასში და მის ქვეკლასში (შვილში).

თუმცა, როგორც `private` მიუწვდომელია კლასის გარედან.

```TS
class Vehicle {
  protected type: string;

  constructor(type: string) {
    this.type = type;
  }
}

class Car extends Vehicle {
  constructor(type: string) {
    super(type);
  }

  public displayType() {
    console.log(`The vehicle type is ${this.type}`);
  }
}

const vehicle = new Vehicle("Truck");
console.log(vehicle.type);  // Error: Property 'type' is protected and only accessible within class 'Vehicle' and its subclasses.

const car = new Car("Sedan");
car.displayType();

```

## Encapsulation

`TypeScript`-ში `getter` და `setter` არიან სპეციალური მეთოდები, რომლებიც განსაზღვრავენ, როგორ მოხდება კლასის თვისებების წამოღება და შეცვლა.

```TS
class Rectangle {
  private _width: number;
  private _height: number;

  constructor(width: number, height: number) {
    this._width = width;
    this._height = height;
  }

  // Getter for area
  get area(): number {
    return this._width * this._height;
  }

  // Setter for width
  set width(value: number) {
    this._width = value;
  }

  // Setter for height
  set height(value: number) {
    this._height = value;
  }
}

const rectangle = new Rectangle(5, 10);
console.log(rectangle.area);  // Getter: 50

rectangle.width = 7;          // Setter: Updates width
rectangle.height = 12;        // Setter: Updates height
console.log(rectangle.area);  // Getter: 84

```

> setter და getter ფუნქციები შეგვიძლია გამოვიძახოთ როგორც ჩვეულებრივი ცვლადები

# Interface

`TypeScript`-ში ინტერფეისები არის მძლავრი ფუნქცია, რომელიც გამოიყენება ობიექტების ფორმის დასადგენად და კოდში ქმნის გარკვეულ სტრუქტურას. მასში შეგვიძლია მივუთითოთ თუ რა თვისებები და მეთოდები უნდა ჰქონდეს ობიექტს ან ობიექტს.

```TS
interface ICustom_Class {
  AddItem(new_value: number): void;
  RemoveItem(value: number): void;
  get GetAllItems(): number[];
}
```

# Generics

ჩვენ შეგვიძლია მოგვიწიოს რიცხვების, სტრინგების, ან ბულინის მასივის შექმნა. ამიტომ სტატიკურად ვერ მივუთითებთ ტიპს. ვერც გამოვიყენებთ `any`-ს, რადგან მაგალითად რიცხვებთან ერთად შეგვიძლია ბულინის დამატებაც, რაც შეცდომაა. `Union` ტიპებთანაც იგივე პრობლემა გვექნება და წინასწარ ვერ განვსაზღვრავთ ყველა საჭირო ტიპს.

მსგავსი გამოწვევების გადასაჭრელად შეიქმნა ჯენერიქები. ჯენერიკები ქმნიან ისეთ კომპონენტებს, რომლებსაც შეუძლიათ იმუშაონ ნებისმიერ ტიპთან, ამავდროულად ინარჩუნებენ ინფორმაციას გამოყენებული ტიპის შესახებ.

## Generic Function

```TS
function identity<T>(arg: T): T {
  return arg;
}

const result1 = identity(5);        // type of result1 is number
const result2 = identity("hello");  // type of result2 is string
```

შეგვიძლია მივუთითოთ ნებისმიერი სახელი, რომელიც მიიღებს ტიპს, ხშირან პირველს აღნიშნავენ როგორც `T`-ს და მეორეს `U`-დ. ფუნქციის გამოძახებისას, ტაიპსკრიპტი გადაცემული მონაცემების მიხედვით შეეცდება გაარკვიოს ჯენერიქის ტიპი. თუმცა, უკეთესი იქნება თუ წინ ხელით მივუთითებთმ თუ რა ტიპებთან ვმუშაობთ, ზედმეტი პრობლემების ასარიდებლად.

შეგვიძლია გადავცეთ ერთ-ზე მეტი ჯენერიქი.

ის არა მარტო ფუნქციებთან გამოიყენება. ასებე ინტერფეისებთან და კლასებთანაც.

## Generic Interface

```TS
interface Box<T> {
  value: T;
}

const box1: Box<number> = { value: 42 };
const box2: Box<string> = { value: "hello" };
```

## Generic Class

```TS
class Container<T> {
  private items: T[] = [];

  add(item: T): void {
    this.items.push(item);
  }

  get(index: number): T {
    return this.items[index];
  }
}

const numberContainer = new Container<number>();
numberContainer.add(1);
numberContainer.add(2);

const stringContainer = new Container<string>();
stringContainer.add("hello");
stringContainer.add("world");
```

# Decorators

დეკორატორი არის სპეციალური ტიპის ფუნქცია, რომელიც გამოიყენება კლასებისა ან მათი წევრების (როგორიცაა მეთოდები, თვისებები ან აქსესუარები) თვისებების დეკლარაციული წესით შესაცვლელად ან გაფართოებისთვის.

საბედნიეროდ, დეკორატორის ხელით შექმნა იშვიათად გვიწევს. Angular-ში კი გვაქვს უკვე მზა, ჩაშენებული დეკორატორები, როგორებიცაა: `@Component`, `@Input`, `@Output`, `@Injectabnle`, `@HostListener`, `@NgModule` და სხვები, რომლებიც გვხემარებიან აპლიკაციის სტრუქტურისა და ქცევის განსაზღვრაში.
