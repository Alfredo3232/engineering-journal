# Getting Started

* What is Vue JS?
  * Vue JS is Javascript Framework that makes building interactive and reactive web front ends easier
  * Framework - A framework is a third party library that exposes utility functionalities and a set of rules on how to build your javascript application
  * Reactive - usually refers when your app is able to react to user input, update the screen dynamically
  * DOM - Document Object Model
* Different Ways of Using Vue
  * Vue can be used to control parts of HTML pages or entire pages
    * The Widget approach on a multi-page-application, some pages are still rendered on and served by a backend server
  * Vue can also be used to control the entire frontend of a web application
    * Single Page Application approach. Server only sends one HTML page, thereafter, Vue takes over and controls the UI
* Exploring Vue Alternatives
  * Vue JS - Complete component based UI framework, includes most core features. A bit less popular than React & Angular
  * React JS - Lean and focused component based UI library. Certain features like routing are added via community packages
  * Angular - Complete component based UI framework, packed with features. Uses TypeScript. Can be overkill for smaller projects.
* Re-Building the App with Vue
  * Do note that we are doing this through a CDN
  * How to start with Vue
    * 1. Add CDN to your HTML
    * 2. Add a JS file through a script tag
    * 3. In your JS your start Vue with `Vue.createApp()`
  * Vue is the object we have available thanks to our CDN
  * `Vue.createApp()` is how we start a Vue App?
    * This takes in a object inside you add and do various things like
      * `data(){}`
        * Is wrapped in a return {}
        * Inside the return you add properties with  values
      *`Methods: {}`
        * Inside it you add functions
  * At the end of `Vue.createApp()`, you have to specify where part of your html do you want to be controlled and watched by Vue
    * Add `.mount(<ID_HERE>)`

---

# Basic & Core Concepts - DOM Interaction with Vue

* Creating and Connecting Vue App Instances

![IMG_HERE](images/image1.png "image_tooltip")

* This is an example of a Vue small app

* Binding Attributes with the “v-bind” Directive
  * `<a href=”LINK”></a>`
    * Instead of providing a link hardcoded you can do it through vue
      * You can create a property in data instead like this

![IMG_HERE](images/image2.png "image_tooltip")

* In order to use a data property inside a html tag attribute you must first bind it

![IMG_HERE](images/image3.png "image_tooltip")

* In order to use a data property from vue to a html tag attribute you must use

```HTML
v-bind:<attribute>="DATA"
```

* For a shorter syntax of `v-bind:`, you can just simply type `:`, and then after the attribute
* Understanding “methods” in Vue Apps
  * Let's say you have a property inside `data()` called `burger`and you want to use it in your methods function, usually you would need to bind this to let JS know what you are referring to.
    * However is Vue you can just say `this.burger` , burger being a property in data. Vue automatically knows and binds the this to what you are referring to
* Outputting Raw HTML Content with v-html
  * Let’s say you have a data property and that property has a string for example

 ```JS
data(){
  return{
    text: '<h1>Hello</h1>'
  }
}
```

* When you try to input this into your html, it wont work as expected
  * In order to make html string work in a html tag
    * You can do this for example

```HTML
<p v-html>{{ text }}</p>
```

* v-html tells vue that the text inside the p tags are html and not text
  * In Vue it interprets text as text unless told otherwise, this is a really good security feature since it prevents cross-site scripting attacks.

* Understanding Event Binding

```HTML
v-on:<EVENT>="<STUFF>"
```

* The v-on allows you to set up a event listener such as click
* Data Binding + Event Binding = Two-Way Binding
  * v-model is basically two-way binding, meaning we are listening to an event coming out of the input element to the input event and at the same time we are writing the value back to the input element through its value property. In shorter words it's like this:

```JS
v-bind:value + v-on:input = v-model
```

* Methods used for Data Binding: How it Works
  * NOTE
    * When Vue re-renders the page, Vue also re-executes any methods you have in your HTML for example any methods within curly braces, or with the bind. So in conclusion any non-event bound methods will be re-executed by Vue whenever anything in the screen changes
* Introducing Computed Properties

```JS
computed: {}
```

* This “method”, accepts functions, but the difference between computed and methods are that vue will be aware of computed function’s dependencies and only re-execute them if one of their dependencies change.
  * NOTE
    * Call computed functions like data properties not like method functions. In the HTML don’t execute them like functions, but instead point at them like data properties
* Working with Watchers

 ```JS
watch : {}
```

* This “methods” also accepts functions, but the difference on this one is that it accepts functions that are named after the properties on data(), so whenever that property changes, it fires the function.

```JS
<PROPERTY_NAME>(newValue, oldValue){ //CODE }
```

* Methods vs Computed vs Watchers
  * Methods
    * Use with event binding OR data binding
    * Data binding: Method is executed for every “re-render” cycle of the component
    * Use for events or data that really needs to be re-evaluated all the time
  * Computed
    * Use with data binding
    * Computed properties are only re-evaluated if one of their “used values” are changed
    * Use for data that depends on other data
  * Watch
    * Not used directly in template
    * Allows you to run any code in reaction to some changed data (e.g. send Http request etc.)
    * Use for any non-data update you want to make
* v-bind and v-on Shorthands
  * We could use v-on, however there is a shorthand for v-on and that is a @, for example
    * OLD -

```HTML
v-on:<EVENT>="<FUNCTION>"
```

* NEW -

```HTML
@<EVENT>="<FUNCTION>"
```

* We could use v-bind, however there is also a shortcut for this
  * OLD -

```HTML
v-bind:<ATTRIBUTE>="<VALUE>"
```

* NEW -

```HTML
:<ATTRIBUTE>="<VALUE>"
```

* Dynamic Styling with Inline Styles

```JS
:style="{borderColor: boxASelected ? 'red': '#ccc' }"
```

* This is an example of a inline style
  * With this styling we can add conditions to what sort of CSS it will render according to what parameter we are setting it to for example the code on top ^
    * We set a ternary operator and it will render red if its true or gray

* Adding CSS classes Dynamically
  * Adding inline styles directly in our HTML is not a very good thing to do because this usually overrides any CSS that we might need, therefore to make it easier and better we add CSS classes dynamically
  * You can set a class dynamically for example

```JS
:class="{active: boxASelected}"
```

* active is a css class  and it renders according if boxASelected is true or not

* Classes & Computed Properties
  * You can use computed properties can be helpful for adding CSS classes dynamically instead of adding logic directly in the HTML code you can just add a property instead
    * For example we could write the code above in a better way
    * HTML Side -

```JS
:class= "boxAClasses"
```

* JS Side

```JS
boxAClasses() {
    return {active: this.boxASelected};
}
```

* This is especially helpful if your code is become really complex depending if it changes dynamically

* Dynamic Classes: Array Syntax

```JS
:class= "[ '<CLASS>', {<EXPRESSION>}]"
```

* With the array syntax you can add multiple classes and expressions

---

# Rendering Conditional Content & Lists

* Rendering Content Conditionally
  * In order to render content conditionally you need to declare it like for example

```JS
<p v-if="true">EXAMPLE</p>
```

* This will render according if the value given is true
  * You can additionally add a v-else-if, this will render if v-if above it is false.
    * And finally v-else will render if any element with v-if or v-else-if is false

* Using v-show Instead of v-if
  * v-show does not work with v-if, v-else-if or with v-else, meaning if you want multiple conditional renders then you will have to add more v-shows
  * Differences between v-show and v-if
    * v-if removes and adds elements from and to the DOM
      * CONS-
        * Adding and removing elements can cost performance
      * PROS-
        * A cleaner and more readable DOM
    * v-show just hides and shows items with css
      * CONS-
        * Cluttered DOM
      * PROS-
        * Better performance
  * You should typically use v-if and use v-show if you have a element that it’s visibility changes a lot
* Rendering Lists of Data

```JS
v-for="<VAR> in <DATA_PROPERTY>"
```

* This is like a for loop in JS, it iterates over an array, and displays every value in the data property you give it
  * `v-for="(&lt;VALUE>, &lt;INDEX>) in &lt;DATA_PROPERTY>"`
  * You can also get the index, not only the value, of course you can name both the value and index to anything that you want
  * v-for also supports objects, you can also extract the key and value exactly the same as you would in a array

* Lists & Keys

```JS
:key=""
```

* You might encounter bugs due to how Vue handles re rendering lists in v-for. The key keeps track of what you want to track, usually you want to track in a v-for the VALUE property.
  * USE `:key=""`, when using v-for to avoid bugs

---

# Course Project: The Monster Slayer Game

* Project Setup & First Methods
  * You can also call other methods, not just data properties. Like data properties you do need this keyword for example, `this.function()`.

---

# Vue: Behind the Scenes

* An Introduction to Vue’s Reactivity
    *
