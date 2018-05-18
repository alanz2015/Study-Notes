# NativeScript Vue.js Template

This repo serves as the starting point for NativeScript + Vue.js projects, using [nativescript-vue](https://github.com/rigor789/nativescript-vue).

## Usage

1.  Install NativeScript tools (see http://docs.nativescript.org/start/quick-setup)

2.  Create app from this template

```bash
tns create hello-ns-vue --template nativescript-vue-template

cd hello-ns-vue
```

> While the `nativescript-vue` project is not up-to-date on npm, you may have to run
> `npm link nativescript-vue` in the project folder (like [described here](https://github.com/rigor789/nativescript-vue/blob/master/CONTRIBUTING.md)).

3.  Run in Android or iOS

```bash
tns run android
tns run ios
```

## Templates

This template contains a number of app samples that you can use as the starting point of your app. To experiment, try copying and pasting the code from `app-with-list-view.js`, `app-with-router.js`, `app-with-tab-view.js`, or `app-with-vmodel.js` into your app’s `app.js` file.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~


Vue Component Structure
=======================
.../src/App.vue file (or main.js in nativescript-vue). This file is our root component.
These component files ending in .vue are single file components.

    * template - This is where our HTML is placed. We can also define non-HTML elements here, but we'll get to that later..
    * script - This is where the logic of our app resides.
    * style - This is where our CSS is placed.

Vue Templating --- Interpolation and Directives
===============================================
Within the <template></template> section of your Vue components, you're able to write HTML and utilize Vue-specific templating features, which are grouped into 2 categories:

    * Vue Interpolations
    * Vue Directives

Vue Interpolations
------------------
    * To use interpolation double curly braces {{ }} with the name of the property inside template. Ex.
	<template>
	  <div class="skills">
	    {{name}}
	  </div>
	</template>
    * To use the v-bind directive, followed by the name of the attribute, and bind it to a property defined in the component logic. Ex.
	<button v-on:click="changeName" v-bind:disabled="btnState">Change Name</button>
    * Expressions in Interpolation. Ex.
	Within interpolation braces, you can place JavaScript expressions.
	{{ btnState ? 'The button is disabled' : 'The button is active'}}

Vue Directives
--------------
A Vue Directive is a Vue-specific attribute prefixed by a v-. Each serve a different purpose. 
    v-text, v-html, v-show, v-if, v-else, v-else-if, v-for, v-on, v-bind, v-model, v-pre,
    v-cloak, v-once
    Ex. v-for is used for iterating through a list.
    data() {
        return {
            skills: [
                {"skill": "Vue.js"},
                {"skill": "Frontend Developer"}
            ]
        }
    },
    ..................
    <li v-for="(data, index) in skills" :key='index'>{{index}}. {{data.skill}}</li>
    <p v-if="skills.length >= 1">You have more than 1 skill</p>
    <p v-else>You have less than or equal to 1 skill</p>



Understanding Scoped in Vue
===========================
<style scoped> : This means that any CSS defined in this component, will only apply to the template in this component.
Linking to an external Stylesheet in Vue: 
    <style src="./Skills.css" scoped>
	ul {
	    list-style-type: none;
	}
	li {
	    font-weight:bold;
	}
        .........
    </style>

Vue Class Binding
-----------------
Both class and style binding in Vue use the v-bind directive. This directive allows you to dynamically control when and if CSS classes and styles are applied, along with CSS properties and values.
To use v-bind on the class attribute as following:
    <div v-bind:class="{ alert: showAlert}"></div> 
Then add the showAlert property in the component logic section:
  data() {
    return {
      skills: [
          { "skill": "Vue.js" },
          { "skill": "Frontend Developer" }
      ],
      showAlert: true  // Add this
    }
  },
And then, add the .alert class in the styles section:
    <style scoped>
	.alert {
	    background-color: yellow;
	    width:100%;
	    height: 30px;
	}
    </style>

Multiple Class Binding in Vue
-----------------------------
For example, to simply separate the classes and properties with a comma, simply define another boolean property in the component logic, and define the .another-class in the styles.
    <div v-bind:class="{ alert: showAlert, 'another-class': showClass }"></div>

Using v-bind:class with an Object
---------------------------------
If you want to keep your component template more clean, you can do the following:
    <div v-bind:class="alertObject"></div>

Then in the component logic:
    data() {
      return {
        skills: [
            { "skill": "Vue.js" },
            { "skill": "Frontend Developer" }
        ],
        alertObject: {
          alert: true,
          // More classes here if you want..
        }
      }
    },

Vue Style Binding
-----------------
Style binding in Vue allows you to control specific CSS properties by using the v-bind directive on the style attribute.
    <div v-bind:style="{ backgroundColor: bgColor, width: bgWidth, height: bgHeight }"></div>

In the component logic, adjust to:
    data() {
      return {
        skills: [
            { "skill": "Vue.js" },
            { "skill": "Frontend Developer" }
        ],
        bgColor: 'yellow',
        bgWidth: '100%',
        bgHeight: '30px'
      }
    },

To make more clean in the component template, just do:
    <div v-bind:style="alertObject"></div>
and adjust the component logic like so:
    alertObject: {
       bgColor: 'yellow',
       bgWidth: '100%',
       bgHeight: '30px'
    }

Vue Form --- Capturing and Validating User Input
================================================
Handling user input with Vue.js is fairly straight forward. With the help of the v-model directive and one of several vue validation plugins for form validation.

Vue V-Model Directive
---------------------
When you need to capture user input, you can use the v-model directive on form inputs and textareas, which enables 2-way data binding. Ex.
    <template>
      <div class="container">

      <!-- Add these two lines: -->
      <input type="text" placeholder="Enter a skill you have.." v-model="skill">
        {{ skill }}
    ...............
Then add the following code in <script>:
    data() {
        return {
          skill: '',  // Add this line
          skills: [
              { "skill": "Vue.js" },
              { "skill": "Frontend Developer" }
          ]
        }
    },

And also style the input button in CSS section as following:
    input {
        width: calc(100% - 40px);
        border: 0;
        padding: 20px;
        font-size: 1.3em;
        background-color: #323333;
        color: #687F7F;
    }

Form Submission in Vue
----------------------
Wrap user input with a form element.
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.."  v-model="skill">
    </form>

We use @submit.prevent, which submits the form and prevents a page reload, and bind it to a method called 'addSkill'. Let's define addSkill as a method in our component logic:
    export default {
      name: 'Skills',
      data() {
        // Removed for brevity
      },

      // Add this section:
      methods : {
          addSkill(){
              this.skills.push({skill: this.skill});
              this.skill = '';
          }
      }
    }

Handling Multiple User Inputs
-----------------------------
Modify the template as shown:
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.."  v-model="skill">

      <!-- Add this line -->
      <input type="checkbox" id="checkbox" v-model="checked">

    </form>

In the script section add:
    return {
      checked: false,   // Add this, it sets the checked property to false
      skill: '',

Then, update the addSkill() method:
      addSkill(){
          this.skills.push({skill: this.skill});
          this.skill = '';
          console.log('The checkbox value is: '+this.checked)  // Add this
      }

Vue Form Validation
https://github.com/baianat/vee-validate
---------------------------------------
A popular validation package is called VeeValidate. VeeValidate is a powerful plugin with a lot of options. Ex.
    <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill">
    <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>

Add CSS ruleset for .alert
  .alert {
    background: #fdf2ce;
    font-weight: bold;
    display: inline-block;
    padding: 5px;
    margin-top: -20px;
  }

Then, add some logic in addSkill():
      addSkill() {
        this.$validator.validateAll().then((result) => {
          if (result) {
            this.skills.push({skill: this.skill});
            this.skill = '';
          } else {
            console.log('Not valid');
          }
        })
      }


Vue Animation
=============
Vue 2 offers the ability to integrate enter & leave animations, along with state transitions.

Enter and Leave Animations in Vue
---------------------------------
Perhaps the biggest use case for Vue animations are based on when given elements enter and leave the DOM. Ex.
    <form @submit.prevent="addSkill">
      <input type="text" placeholder="Enter a skill you have.." v-model="skill" v-validate="'min:5'" name="skill" >

      <!-- Add these 3 lines -->
      <transition name="alert-in">
        <p class="alert" v-if="errors.has('skill')">{{ errors.first('skill') }}</p>
      </transition>
      ..............
    </form>

The important part to note here is the transition wrapper component.
The transition wrapper will apply animations in the following cases based on what's being wrapped within:

    * v-if conditional rendering
    * v-show conditional display
    * dynamic components
    * component root nodes

In our case, the <p class="alert" ... element has a v-if directive applied to it already.





What is the concepts of "template" and "plugin"? What is the "page" meaning in app.js?
How to separate production and development revision?
For a integration of vue and nativescript, which parts are nativescript, and which parts are vue?
