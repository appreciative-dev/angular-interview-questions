# What are Observables?
Observables are asynchronous streams that produce data over time.

# What are Generics?
Generics allow creating 'type variables' which can be used to create classes, functions & type aliases that don't need to explicitly define the types that they use.

# What are Union types?
Union types are used when a value can be more than a single type. Using the | we are saying our parameter is a string or number.

# What are Abstract classes?
Abstract classes are mainly for inheritance where other classes may derive from them.
We cannot create an instance of an abstract class.

```
abstract class Animal<C extends string | string[]> {
  public abstract communicate(communication: C): void;
}
```

# What are function declaration(definition) and expression?
- Expression is similar to a function declaration without the function name.
- Function declaration does not require a variable assignment and are executed before any other code - hoisting

# What is a typeof operator?
```
const myFunction = (a, b) => a + b
console.log(typeof myFunction); // function
```

```
var bar = null;
console.log(typeof bar === "object"); // logs true!
null is also considered an object
```

# What is IIFE - imidiatly invoked function expression?
()() - means that a function will be called just after initialization\

```
(function () {
  // …
})();
```

# What is a static keyword?
When we use the static keyword on properties we define on a class, they belong to the class itself.
That means that we cannot access those properties from an instance of the class.

```
class Vinyl {
  public static NUM_VINYL_CREATED: number = 0;
  constructor (title: string, artist: string, genres: Genre[]) {
    Vinyl.NUM_VINYL_CREATED++; // increment number of vinyl created
    console.log(Vinyl.NUM_VINYL_CREATED)
  }
}
let goo = new Vinyl ();
goo.NUM_VINYL_CREATED // Error
```

# What is a protected keyword?
protected access modifier is similar to the private access modifier, except that protected members can be accessed using their deriving classes (keyword extends).

# Describe variable scope.
Variables defined with let and const are hoisted to the top of the block, but not initialized./
var is hoisted. Their initial value is undefined/
Since when the let expression is used, every iteration creates a new lexical scope chained up to the previous scope. /Deeply-nested scopes may be the reason for lower performance in this case./
- var: function scoped
- let, const: block scoped

# Describe a closure.
closure - a variable stores in heap memory instead of call stack. it's available inside the scope and inner scopes, but unavilable outside.

```
function getDate () {
  var date = new Date()
  return date
}
console.log(getDate()) // logs Time
console.log(date) // ERROR
```

# Describe a Unit testing, give a example.
Unit testing is a software development process in which the smallest testable parts of an application, called units.
beforeEach method is a feature that you can use to set preconditions for each test.
fixture is a wrapper for a component and its template.
TestBed is a mock environment to run tests (kind of API).

```
fixture = TestBed.createComponent(QuotesComponent);
component = fixture.componentInstance;
```

--or--

```
element = fixture.nativeElement.querySelector('p');
element = fixture.nativeElement.query(By.css('p'));
debugElement abstraction to work safely across all supported platforms.
```

toBe - primitives/
toEqual - object/
toMatch - string/
toContain - array/
you can write a method on a component and can access this method in the test block

```
service = Testbed.inject(FakeService)
spyOn objects simulate how fetchFromServer works
spyOn(quoteService, "fetchQuotesFromServer").and.returnValue(
  Promise.resolve(fakedFetchedList)
);
```
spyOn get 2 params: a service a a method
when use async call you should pass a done param to 'it'

to create fakeservice use jest.fn()
providers: [{ provide: UserService, useClass: UserService}]
a separate class that will be able to implement the methods in a different way

# What is a difference between JIT and AOT?
- Just-in-Time (JIT) compiles in the browser at runtime.
- Ahead-of-Time (AOT) compiles app at build time./
AOT significantly reduces the bootstrapping time of the app, it is smaller and security is increased, but take more time to compile

# What is a factory function?
A factory function can be defined as a function that creates an object and returns it. It is similar to constructor functions/class functions.

# What is a DI?
DI means passing dependent object as parameter to a method, instead a method creating a dependent object. This method doesnt have a direct dependency on a particular implementation - we depends more on abstarction than on concrete implementation

# Describe an injection.
```
constructor(public engine: Engine) {}
same as constructor(@Inject(Engine) engine:Engine)
```

for primitives:
```
export const APP_CONFIG = new InjectionToken<AppConfig>('app.config');
providers: [{ provide: APP_CONFIG, useValue: HERO_DI_CONFIG }]
constructor(@Inject(APP_CONFIG) config: AppConfig) {
  this.title = config.title;
}
```

new inject from Angular 14. service = inject(SomeService). //here can be a method from inside service be opened
you can use the inject() function in Pipes and Directives aswell
if you use the inject() function you dont even need a service as a dependency in your component

# Describe useExisting, useClass and etc.
useExisting - create refrence to an existing service
useClass - create new instance of service.
Use this type of provider to substitute an alternative implementation for a common or default class.
{ provide: Class1, useClass: Class3 } - when a constructor requests Class1, DI creates an instance of Class3 and passes it to the constructor.
The alternative implementation can, for example, implement a different strategy, extend the default class, or emulate the behavior of the real class in a test case.

multi: true used to register multiple services or values with one token. Returns an array with all services or values.
If to forget put multi: true then it will overrides the previously registered directives.

# Describe a Node Injector Tree.
If the component injector can not resolve the token, Angular travels up its parents nodes.
- @SkipSelf() - Skips itself and starts with the parent component injector
- @Self() - Only looks on the current component injector
- @Optional() - Returns null instead of throwing an error if no provider is found
- @Host() - Even if there is a service instance further up the tree (from the parent), Angular wont continue looking

# What is a Tree shaking?
Tree shaking is a way to eliminate unused modules from the final bundle file of the application. Services in the NgModule providers array or at component level are not tree-shakable.

# What is a viewProviders?
ViewProviders - All child components within ng-content dont see the provider./
This can be used to make a service private since it s not exposed to its content children.
```
viewProviders: [
  { provide: ControlContainer, useExisting: FormGroupDirective },
],
```

# What is a npx?
A package can be executable without installing the package. npx is a tool that use to execute packages.

# Describe how prisma works in NestJS.
- npx prisma migrate - creates tables in db according to the model
- npx prisma generate - create a ts structure/
- npx prisma studio - opens a ui for admin a db/
- PrismaClient is a class to connect to db and make queries. To wire OneToMany relations among entities, you have to mark a property with @relation and and bonded fields on Conroller we could pass only value according to a model, using whiteList: true inside useGlobalPipes(new ValidationPipe)

# Describe an event loop.
The functions that finished the Web Apis execution are being moved to the Callback Queue, this is a regular queue data structure.
Event Loop is responsible for dequeuing the next function from the Callback Queue and sending the function to the call stack to execute the function.
To be more accurate there are actually two types of queues.
- Common Macro-Tasks are setTimeout, setInterval, and setImmediate.
- Common Micro-Task are process.nextTick and Promise callback.
https://medium.com/gradeup/asynchronous-javascript-event-loop-1c8de41298dd

# Describe an order of execution inside event loop
All functions that are currently in the call stack get executed and then they get popped off the call-stack.
When the call stack is empty, all queued-up micro-tasks are popped onto the call-stack one by one and get executed, and then they get popped off the call-stack.
When both the call-stack and micro-task queue are empty, all queued-up macro-tasks are popped onto the call-stack one by one and get executed, and then they get popped off the call-stack.

# What is a stack?
This stack lives during the execution of the function, once the function finished its code - the stack is being removed.
Think about the heap as part of the memory, that is related to the process and not to a specific function, which means there can be many stacks because there are many functions but there is only 1 heap.
It means that references are stored in the stack during the function execution, and values are stored in the heap.

# Describe a difference between higher order function and callback function.
- a function which takes another function as an argument or returns a function is known as a higher order function
- callback function means just a function will be passed as an argument (and not necessary to return)

# Describe a difference between a session and token handling?
- session is handled on the server and token on the client, token is stored in http headers
- stateful - just auth id and other info on the server, token - all info is stored in token

# What is a CORS?
The CORS behavior, commonly termed as CORS error, is a mechanism to restrict users from accessing shared resources.
The CORS standard works by adding new HTTP headers which allow servers to serve resources to permitted origin domains.
Browsers support these headers and respect the restrictions they establish.
And let's assume that a page you server from my-cool-site.com made a request to third-party-site.com.
Normally, users browser will decline AJAX calls to any other site other than your own domain/subdomain per the Same-Origin Security Policy. But if the browser and the third party server supports CORS, the following things happen:

```
Origin: https://foo.example
Access-Control-Allow-Origin: https://foo.example
Access-Control-Allow-Origin: \*
also types of requests can be attached (server conf)
```

# What is an abstraction, inheritance, encapsulation, and polymorphism?
1. abstraction - to simplyfy a usage we hide realization
2. inheritance - we can inherit properties and methods from a parent class (the same behavior)
3. encapsulation - using public and private we can give an access to properties from outside of the class
4. polymorphism - we gain the ability for different possible implementations, reusing a single piece of code multiple times

# Describe a SOLID
1. Single Responsibility
2. Open Close
3. Liskov Substitution
4. Interface Segregation
5. Dependency Inversion

# Describe an example of lazy loading?

```
{ path: ‘user’, loadChildren: () => import(‘./users/user.module’).then(m => m.UserModule) };
```

# What is a polyfill?
polyfill is a piece of code that implements features that are not supported by the current browser

# Describe a security in Angular.
Angular sanitizes and escapes untrusted values When a value is inserted into the DOM from a template, via property, attribute, style, class binding, or interpolation.
The offline template compiler prevents vulnerabilities caused by template injection (AOT).
Sanitization is the inspection of an untrusted value, turning it into a value that's safe to insert into the DOM
You can inject DomSanitizer in component as parameter in constructor. this.trustedUrl = DomSanitizer.bypassSecurityTrustUrl(this.dangerousUrl);
built-in browser DOM APIs or methods don't automatically protect you from security vulnerabilities
Angular has built-in support for preventing http level vulnerabilities such as as cross-site request forgery (CSRF or XSRF) and cross-site script inclusion (XSSI)

# What is a xss attack?
In this instance, the interpolation mechanism in Angular will escape your input. It won't interpret the input as HTML and will display the entire input as plain text on your webpage.
This defense mechanism in Angular is known as "contextual escaping."
Angular has automatically recognized the ```<script>``` tag as unsafe and removed it, but has kept the ```<b>``` tag as it's potentially safe.
This modification in Angular is called "sanitization."
you can make use of the DomSanitizer and use the byPassSecurityTrust..() functions to tell Angular that you trust the input value

# How to prevent app from crashing if a property in an object is accessed, but not defined?
optional chaining ``` propertyName?.propertyName ```

# What is a standalone component?
A standalone component is a type of component which is not part of any Angular module
```
@Component({
  standalone: true
})
```

# Describe a difference between a impure and pure pipe?
Angular calls an impure pipe for each change detection cycle, independent of the change in the input fields.
- when you pass an array or object that got the content changed (but is still the same instance)
- when the pipe injects a service to get access to other values, Angular doesn't recognize if they have changed.

```
@Pipe({
  name: 'somePipe',
  pure: false/true
})
```
- If pipe is pure: there will be only one instance of the pipe. The transform method will be called twice but on the same instance.
- If pipe is impure: there will be two instances of the pipe

# How to opimize SEO?
Angular Universal provides a server-side rendering, it loads faster and has better SEO

# Describe a View encapsulation.
View encapsulation specifies if the component's template and styles
1. Native: The component does not inherit styles from the main HTML
2. Emulated (Default): The component inherits styles from the main HTML
3. None: The component's styles are propagated back to the main HTML and therefore accessible to all components on the page

# Describe a NgZone.
- NgZone.onMicroTaskEmpty() is called ApplicationRef.tick() is called then - it leads to call a detectChanges() on every view
- ngZone.runOutsideAngular - runs outside zone for performance crucial code
- ngZone.run - run inside zone to make view updates
- there ways (requestAnimationFrame, on_property, BLACK_LISTED_EVENTS) to disable changes inside zone

# Describe a ChangeDetectionStrategy.
- ChangeDetectionStrategy.Default, Angular will have no assumption on the component’s dependency and will check every component from the component tree from top to bottom every time an event triggers change detection on browser events, timers, XHRs, and promises.
- ChangeDetectionStrategy.Push - Input, events, async pipe, ChangeDetectionRef

# Describe a function context
- bind - return a function with new context
- call, apply - call a function with new context

# Describe a difference between em and rem?
em depends on parent, rem depends on root

# How to write a custom input?
```
interface ControlValueAccessor {
  writeValue(obj: any): void
  registerOnChange(fn: any): void
  registerOnTouched(fn: any): void
  setDisabledState(isDisabled: boolean)?: void
}
```

# Describe a difference between rebase and merge.
rebase rewrites commits (with changing a history) and put them on top of other commits (no new commit will be created), it moves feature commit on top of new changes from master

# Describe a @ViewChild.
- ``static:true`` will resolves ViewChild before any change detection is run. default - ``static: false`` will resolves it after every change detection run.
- read: Use it to read the different token from the queried elements.

```
@ViewChild("sayHelloTemplate", { static: false }) tempRef: TemplateRef;
```

```
<ng-template #sayHelloTemplate>
  <p> Say Hello</p>
</ng-template>
```

```
constructor(private vref:ViewContainerRef) {}
ngAfterViewInit() {
  this.vref.createEmbeddedView(this.sayHelloTemplate);
}
```


```
<ng-content select="header"></ng-content>
<app-card>
 <header><h1>Angular</h1></header>
</app-card>
```

# How to catch a false condition in *ngIf?
```
*ngIf="selected; then thenBlock1 else elseBlock1"
```

# Describe lifestyle hooks.
1. ngDoCheck: This is fired each time anything that can trigger change detection has fired (e.g. click handlers, HTTP requests, route changes, etc…). This lifecycle hook is mostly used for debug purposes;
2. ngAfterContentInit: called after external content has been projected into the component. Remember content queries like @ContentChildren and @ContentChild are set before the hook callback is called;
3. ngAfterContentChecked: called after every check of component content;
4. ngAfterViewInit: called after component’s view(s) are initialized. Perfect for initializing event third party library, that needs the view be composed before taking any action (note that a view differs from content because a components view is the non-projected template);
5. ngAfterViewChecked: called after every check of a component’s view(s);

# Describe a difference between flex-wrap, flex-flow and align-content.
- flex-wrap. By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property.
- flex-flow. This is a shorthand for the flex-direction and flex-wrap properties
- align-content is for multi line flexible boxes, determines the spacing between lines

# Describe types Partial, Record, Omit, Pick.
```
interface Point {
  x: number;
  y: number;
}
let pointPart: Partial<Point> = {}; // `Partial` allows x and y to be optional
pointPart.x = 10;
```

```
const nameAgeMap: Record<string, number> = {
  'Alice': 21,
  'Bob': 25
};
Record<string, number> is equivalent to { [key: string]: number }
```

```
interface Person {
  name: string;
  age: number;
  location?: string;
}
const bob: Omit<Person, 'age' | 'location'> = {
  name: 'Bob'
  // `Omit` has removed age and location from the type and they can't be defined here
  // `Exclude` removes from type alias, not from Interface
};
const bob: Pick<Person, 'name'> = {
  name: 'Bob'
  // `Pick` has only kept name, so age and location were removed from the type and they can't be defined here
};
```

# What is a prototype?
The prototype is an object that is associated with every functions and objects by default in JavaScript, where function's prototype property is accessible and modifiable and object's prototype property (aka attribute) is not visible. Every function includes prototype object by default.

```
function Animal (name, energy) {
  // const this = Object.create(Animal.prototype)
  this.name = name
  this.energy = energy
  // return this
}
// const leo = Animal('Leo', 7) - we use new instead
const snoop = new Animal('Snoop', 10)
```

Every object which is created using literal syntax or constructor syntax with the new keyword,
includes ```**proto**``` property that points to prototype object of a function that created this object

# Describe a composition.
composition (has a) over inheritance (is a)
https://www.youtube.com/watch?v=rcDsRyVhcxY

# How to access a css variable insde child elemt
write inside the class element on the child element

```
.some-class {
  :host-context(.theme-red) & {
    color: green;
  }
}
```

and we are adding class="theme-red" on the parrent element
or we can define a variable inside parrent

```
:host {
  --some-var
}
and then inside child
.some-class {
  color: var(--some-var);
}
```

# Describe the following.
1. access any properties on values with the type unknown
2. How WeakMap allows to use to define a property as private
3. pristine, dirty, touched for input element
4. integration Angular with Figma
5. GraphQL
6. https://angular.io/guide/workspace-config
7. https://blog.thoughtram.io/categories/angular/
8. SonarQube
9. Richardson Maturity Model
10. shadowDOM
11. ::ng-deep

# How resolve following example and others (leetcode)

```
function fac(n) {
  if (n==1) {
    return 1
  } else {
    return n * fac(n-1)
  }
}
```

```
function fac2(n) {
  let res = 1
  for (let i = n; i>=1; i--) {
    res = res * i
  }
  return res
}
```

```
function checkPalindrom (str) {
  return str === str.split('').reverse().join('')
}
```
