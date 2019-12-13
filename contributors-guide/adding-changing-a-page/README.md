# Creating and populating a page \(exercise\)

## Objectives

To create a new page, accessible from the navbar with a given icon

The page will first uses event handling to dynamically  animate text. 

The page will then calls an external web-service \(wikipedia API\) to populate and animate content. 

## Steps to follow

### 

### Optional challenge : make it prettier

The current version of the new page isn't very visually appealing. This challenge is to make the page looking like a web startup front page. 

Somethings that says _"We are so amazing you wouldn't even understand" ._ Look at [startup generator](http://tiffzhang.com/startup) if you need inspiration.

To that end, you can use two features of OnsenUI, **page background** and **cards**. 

#### Page background

The v-ons-page component comes with a easy to use background effect. To use it, simply add a new children div where `class="background"` This will be interpreted as a static background. 

```javascript
<template>
  <v-ons-page>
      <div class="background">
          <img src="https://wi-images.condecdn.net/image/zgdPJmnE1aW/crop/1620/f/situational_wired_improbable_26-04-17_239_v1rgb-copy.jpg"/>
      </div>
      
      <div class="content">
          Hello page
      </div>
  </v-ons-page>
</template>
```

#### Cards components

OnsenUI card component \([v-ons-card](https://onsen.io/v2/api/vue/v-ons-card.html)\) permit to group related information.  Cards have a **title** and a **content.** Title and content are div where `class="title"` and `class="content"` respectively.

```javascript
      <v-ons-card>
        <div class="title">Awsome</div>
        
        <div class="content">
          Lorem ipsum dolor, sit amet consects.
        </div>
      
      </v-ons-card>

```



### Introducing reactivity : dynamic number of observations

After having created static content, we will now use this content to use reactivity. Reactivity is at the core of VueJS. 

{% hint style="info" %}
Beyond Albiziapp and VueJS, reactive programming is a research topic in itself \(that has relations with MDE although no clear consensus exists\).
{% endhint %}

In the case of Albiziapp, reactivity means :

* Data are declarative. The UI reacts automatically to data change.
  * =&gt; The UI should not change if there are no data change
* Derived data are bounded to the original data. 
  * If `a=b+c`  each time `b or c` are changed, a will change accordingly.
* Data changes occurring in a subcomponent are reflected in the parent components

#### Practical example : mutating data

In the new page script, let's declare a `data()` function. This function is used in VueJS to create simple reactive data. For convenience, use the following code.

```javascript
<template>
  <v-ons-page>
    <div class="content center">{{text}}</div>
  </v-ons-page>
</template>

<script>
export default {
  data() {
    return {
      text: "interest"
    };
  }
};
</script>

<style>
.center {
  position: relative;
  top: 50%;
  left: 50%;
}
</style>

```

The `text` variable is here declared and initialized. It is now possible to refer to `text` in the UI. The`{{text}}` item in the div is a simple illustration of this use. 

The double mustache syntax evaluates the value of the **javascript expression** it contains, and return the string representation of this expression. Practically it gives a lot of power. Replace {{text}} by the following examples.

```javascript
    {{text.toUpperCase()}}
    {{text.split('').sort().join().split('')}}

```

#### Practical example : fetching data from an external source

Data do not have to be defined at creation. Let's explore an example using data recovered from an external source. 

