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

```HTML
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

# Vue: Behind the Scenes l

* An Introduction to Vue’s Reactivity
  * The all of data()’s properties is taken by Vue and merges it to a behind the scenes global object, the same object where your methods are merged into.
* Vue Reactivity: A Deep Dive
  * Javascript is not reactive by default for example

```JS
let message = 'Hello!';
let longMessage = message + 'World!';
console.log(longMessage);
message = 'Hello!!!!';
console.log(longMessage);
```

* Up to the 1 console log it will display as expected ‘Hello!World’ however at the second console log it wont show the new message because  longMessage is at another point in time.
  * What Vue uses is something called new Proxy() this is a native JS feature, that helps an object be “reactive”
* Understanding Templates
  * When vue takes control of a specific part in the HTML that is called a Template
* Working with Refs
  * ref, allows you to retrieve values from DOM elements, when you need them, instead of all the time
  * In order to get access to refs="VARIABLE", you need to reference this -  this.$refs.VARIABLE.VALUE
* How Vue Updates the DOM
  * NOTE
    * These are functions that are outside of method meaning it will be on the root of the app component
  * beforeCreate() {} , This will execute any code before the Vue App is initialized.
  * created() {} , This will execute any code after the Vue app is initialized, but you still won't see anything like beforeCreate because the app has not been mounted yet.
  * beforeMount() {} , This will execute any code right before the app mounts, you still won't see anything rendered on the screen.
  * mounted() {} , This will execute any code after it was mounted, so it will show something on the screen.
  * beforeUpdate() {} , This will execute any code before any code is updated. Meaning this won’t execute when the page is loading.
  * updated() {} , This will execute any code after any code is updated. Meaning this won’t execute when the page is loading.

---

# Introducing Components

* Introducing components
  * Components are great if you have certain HTML code which you reuse on different parts in your HTML, which then you have certain functionality.

```JS
app.component('Words-Words', {
    //this can have any code that a normal vue app would
      like data and methods
});
```
  
* A vue component is essentially another vue app that belongs to another app.

---

# Vue Development Setup & Workflow

* Inspecting the Vue Code & “.vue” files

![alt_text](images/image4.png "image_tooltip")

* In order to start a vue app begin by installing vue cli globally

```bash
npm install -g @vue/cli
```

* Then start an application by running

```bash
vue create <NAME_OF_PROJECT>
```

* NOTE:
  * Vue CLI is in maintenance mode, it is recommended to use [create-vue](https://github.com/vuejs/create-vue)

```bash
npm init vue@3
```

* This starts a project with Vue3, if you need Vue2 then

 ```bash
npm init vue@2
```

* DON’T omit the @number because npm will try to do it itself and will probably install a outdated version of the project
  * In the src folder is where we keep most of our JS and vue code
    * We have a main.js file, inside this is where we actually create our application and mount it to an id of the HTML

![alt_text](images/image5.png "image_tooltip")

* Our vue files are structured like this

```HTML
<template>
  <section>
 <h2>My Friends</h2>
 <ul>
   <li></li>
 </ul>
  </section>
</template>
<script>
  export default {
    data() {
      return {
        friends: [
          {
            id: "jenny",
            name: "Jenny",
            phone: "012 3456 7890",
            email: "jenny@localhost.com",
          },
          {
            id: "john",
            name: "John Wick",
            phone: "098 7654 3210",
            email: "wick@localhost.com",
          },
        ],
      };
    },
  };

</script>
```

* It seems that vue files are capitalized, for example this file is called App.vue
  * It's also common practice to keep HTML relatively clean as possible because components like the HTML code above will be inserted

---

# Component Communication

* Introducing “props” (Parent => Child Communication)
  * To declare props, short for properties. Props are like data properties. Inside the component you can start them like this

```JS
props: [
  'NAME'
]
```

* You can access it anywhere in your component or app like normal this.NAME_HERE a
  * NOTE
    * When declaring your prop values make sure to use camelcase, vue automatically translates props from this propName to this prop-name.

* Prop Behavior & Changing Props
  * Props usually should not be mutated, you shouldn’t mutate the props because Vue uses a concept called “unidirectional data flow”
  * There two ways in changing the value of props
    * One way is to let the parent know that we’d like to change this. Then the parent can change the data in itself and pass the updated data back to the child
      * In the parent set a data property to the prop for example

```JS
copyProp: this.propName
```

* So then as a substitute you can use copyProp as the original prop, without changing the actual prop

* Validating Props
  * Props can also be declared not only in an array but also in this way

```JS
props: {
   NAME1: String,
   NAME2: Number,
   NAME3: {
       type: String,
       required: true
   }
}
```

* You can declare a type of what your prop is going to receive and if it receives anything else it will give out a error
  * It can also receive an object with the property of a String or whatever data type it is, but also it has extra features that are specific, like required.
  * If you set your prop to required: false, a good thing to put is also the default property, so if the prop isn’t given anything it defaults back to the set value.
    * default: VALUE_HERE
    * I am assuming that the default value has to be the same data type that is expected like for example a String
    * In the default you also provide a function to execute when that prop isn’t given a value
  * Another thing that you can provide in the prop object is something called validator and takes in a function for example

![alt_text](images/image6.png "image_tooltip")

* This validator checks if the value that isFavorite receives is either of these two values and will return true or false and will warn you in the console when it isn’t receiving the correct expected values

* Working with Dynamic Prop Values
  * When using v-for in a custom component adding a key is mandatory for example
  * :key=“friend.id”
* Emitting Custom Events (Child => Parent Communication)
  * emits: [], this is how you declare this and you will define which custom events your component will eventually at some point emit.

```JS
emits: ['something in here']
```

* $emit(), Vue $emit is a function that lets us emit, or send, custom events from a child component to its parent. because it is used to notify the parent component that something changed.

* Provide + Inject To The Rescue
  * Provide & inject - A pattern you can use to provide data in one place and inject it (which means use it) in another place.

```JS
provide: { 
  //properties 
}
```

```JS
inject: ['<PROPERTIES_NAME>']
```

*You can only inject what has been provided by a parent component or a ancestor component
    * For provide there is another way to actually instiate it
      * BEFORE -

```JS
provide: {
 <name>: <value>
}
```

* AFTER -

```JS
provide() {
  return {
    <name>: <value>
  }
}
```

* NOTE - You should not always use provide & inject to replace props and custom events. Props and custom events should be your default communication mechanism.
  * NOTE - if you find yourself having some pass through components, for example if you have a component file or multiple components passing through props & passing through the immediate event in such cases using provide & inject can save you some unnecessary code

---

# Diving Deeper Into Components

* Global vs Local Components

```JS
const app = createApp(App)
app.component('name-component', Name)
```

* When we register components like this means that we are registering the component as a Global component. That means that component is available globally in the entire Vue app.
  * When registering components globally means that Vue needs to load them all when the application is loaded initially
  * When registering components locally instead of doing component(), you can import your component to the file that is going to use it.
    * For example:

```JS
import COMPO from './<PATH>'
export default {
  components: {
    'name-compo': COMPO
  }
}
```

* Also for the names of your component you can also use camel case for your name.
  * For example:

```JS
import CompoDos from './<PATH>'
export default {
  components: {
    CompoDos: CompoDos
  }
}
```

* However unlike in the other way we need to declare components like this

```HTML
<CompoDos />
```

* Also you can do it just like this and you can style it both ways &lt;compo-dos> and &lt;CompoDos>

```JS
components: {
  CompoDos
}
```

* Scoped Styles
  * No matter where you put your styling it would always be treated as global styling that affects your entire app

```HTML
<style>
   //CSS HERE
</style>
```

* However there is a way to have the styling only affect the vue file you are on

```HTML
<style scoped>
   //CSS HERE
</style>
```

* NOTE - it only affects the template that lives in the same file and no other component, no child component, no sibling component

* Introducing Slots
  * If you want to create your own component with some specific styling you can do that, for example

```HTML
<template>
  <div>
    {{ content }}
  </div>
</template>

<script>
export default {
  props: ["content"],
};
</script>

<style scoped>
div {
  margin: 2rem auto;
  max-width: 30rem;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  padding: 1rem;
}
</style>
```

* There is a problem here, if you try to use use this component as a wrapper it wont work as expected because Vue doesn’t know what to do with the inside content, you could pass your content through something like this

```HTML
<base-card content="CONTENT_HERE">
</base-card>
```

* However if you pass it through there, you won't be able to have Vue features
  * If you want to pass inside content it won’t be through props it would be through slot
    * You don't need anything in script, you need to use it like this

```HTML
<template>
   <div>
      <slot></slot>
   </div>
</template>
```

* Named Slots
  * If you add different slots vue will throw an error because it doesn't know what you are passing through belongs to what slot.
  * So slots have a attribute called “name”

```HTML
<slot name="NAME"></slot>
```

* This tells vue that you have another slot, you don’t need to name one slot since that is the default, so whatever slot that you don’t name (ONLY ONE UNNAMED SLOT) is the default one.
  * In order to use the named slot, you have to tell vue where you want your content to pass.
    * v-slot:&lt;NAME>
    * v-slot:default
      * This targets the default slot (The one without  a name attribute)
  * Anything within &lt;slot>&lt;/slot>, becomes the default content, meaning that if that slot doesn’t receive any content it displays the content within the slot

* More on Slots
  * To console log slots there is a special property provided one of the ways to see what is inside slots its to console log it in mounted

```JS
mounted() {
   console.log(this.$slots);
}
```

* You can also access and console log individual slots like so

```JS
console.log(this.$slots.default);
```

```JS
console.log(this.$slots.<NAME>)
```

* There is a shortcut for v-slot: and that is the hash. For example
  * OLD:

```HTML
<template v-slot:NAME>
  //code
</template>
```

* NEW:

```HTML
<template #header>
  //code
</template>
```

* Dynamic Components
  * A new and good way to add dynamic components it's through this way

```HTML
<component is="name-component">
</component>
```

* You can actually vBind the is property and dynamically change with a method based on what happens to on your page
  * The old way is through putting the components and attaching a v-if and using it that way
