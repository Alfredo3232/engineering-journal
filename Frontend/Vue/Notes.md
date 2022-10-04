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
        * 3. In your JS your start Vue with Vue.createApp()
    * Vue is the object we have available thanks to our CDN
    * .createApp() is how we start a Vue App?
        * This takes in a object inside you add and do various things like
            * data(){}
                * Is wrapped in a return {}
                * Inside the return you add properties with  values
            * Methods: {}
                * Inside it you add functions
    * At the end of createApp(), you have to specify where part of your html do you want to be controlled and watched by Vue
        * Add .mount(&lt;ID_HERE>)


---


# Basic & Core Concepts - DOM Interaction with Vue



* Creating and Connecting Vue App Instances
    * 

<p id="gdcalert1" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image1.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert2">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image1.png "image_tooltip")

    * This is an example of a Vue small app
* Binding Attributes with the “v-bind” Directive
    * &lt;a href=”LINK”>&lt;/a>
        * Instead of providing a link hardcoded you can do it through vue
            * You can create a property in data instead like this
            * 

<p id="gdcalert2" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image2.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert3">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image2.png "image_tooltip")

    * In order to use a data property inside a html tag attribute you must first bind it
        * 

<p id="gdcalert3" ><span style="color: red; font-weight: bold">>>>>>  gd2md-html alert: inline image link here (to images/image3.png). Store image on your image server and adjust path/filename/extension if necessary. </span><br>(<a href="#">Back to top</a>)(<a href="#gdcalert4">Next alert</a>)<br><span style="color: red; font-weight: bold">>>>>> </span></p>


![alt_text](images/image3.png "image_tooltip")

        * In order to use a data property from vue to a html tag attribute you must use

            ```
v-bind:<attribute>="DATA"
```


            * For a shorter syntax of `v-bind:`, you can just simply type `:`, and then after the attribute 
* Understanding “methods” in Vue Apps
    * Let's say you have a property inside `data()` called `burger `and you want to use it in your methods function, usually you would need to bind this to let JS know what you are referring to.
        * However is Vue you can just say `this.burger` , burger being a property in data. Vue automatically knows and binds the this to what you are referring to
* Outputting Raw HTML Content with v-html
    * Let’s say you have a data property and that property has a string for example

        ```
data(){
  return{
    text: '<h1>Hello</h1>'
  }
}
```


        * When you try to input this into your html, it wont work as expected
    * In order to make html string work in a html tag
        * You can do this for example

            ```
<p v-html>{{ text }}</p>
```


            * v-html tells vue that the text inside the p tags are html and not text
    * In Vue it interprets text as text unless told otherwise, this is a really good security feature since it prevents cross-site scripting attacks.
* Understanding Event Binding

    ```
v-on:<EVENT>="<STUFF>"
```


    * The v-on allows you to set up a event listener such as click 
* Data Binding + Event Binding = Two-Way Binding
    *  v-model is basically two-way binding, meaning we are listening to an event coming out of the input element to the input event and at the same time we are writing the value back to the input element through its value property. In shorter words it's like this:

        ```
v-bind:value + v-on:input = v-model
```


* Methods used for Data Binding: How it Works
    * NOTE
        * When Vue re-renders the page, Vue also re-executes any methods you have in your HTML for example any methods within curly braces, or with the bind. So in conclusion any non-event bound methods will be re-executed by Vue whenever anything in the screen changes
* Introducing Computed Properties

    ```
computed: {}
```


    * This “method”, accepts functions, but the difference between computed and methods are that vue will be aware of computed function’s dependencies and only re-execute them if one of their dependencies change.
    * NOTE
        * Call computed functions like data properties not like method functions. In the HTML don’t execute them like functions, but instead point at them like data properties
* Working with Watchers

    ```
watch : {}
```


    * This “methods” also accepts functions, but the difference on this one is that it accepts functions that are named after the properties on data(), so whenever that property changes, it fires the function.

        ```
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
    * a