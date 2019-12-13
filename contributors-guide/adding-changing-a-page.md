# Creating a new page \(exercise\)

## Objectives

To create a new page, accessible from the navbar with a given icon

 The page will displays in real time the total number of observation. 

A new observation from another user should be reflected immediately in the counter. A new observation from the current user should update the counter.

## Steps to follow

### Start using the tools

* Start Albiziapp locally \(you might have to kill already running albiziapp processes\)

{% hint style="info" %}
Use`vue ui`from the albiziapp/ directory then Task`->`Serve`->`Run task 
{% endhint %}

This action triggers the source dependencies injection, their bundling and then start serving Albiziapp at [http://localhost:8080/](http://localhost:8080/)

![Expected output at http://localhost:8000/](../.gitbook/assets/image%20%281%29.png)

{% hint style="info" %}
From vue-dashboard on top left menu : "open in editor" . It should open VSCode.
{% endhint %}

* Create a .vue file in the pages directory. **The file should start with a capital case**.

This file is first empty. Let's fill it a bit :

{% hint style="info" %}
Use Ctrl-Space to trigger the powerful autocomplete. Chose the first option
{% endhint %}

![](../.gitbook/assets/image%20%286%29.png)

Your Test.vue should now look like below.

```javascript
<template>
  
</template>

<script>
export default {

}
</script>

<style>

</style>
```

Using autocomplete, populate the template. Add the v-ons-page element as direct child of template. Then add something to display for test purposes \(here a div\).

```javascript
<template>
  <v-ons-page>
      <div class="content">Hello page</div>
  </v-ons-page>
</template>
```

### Add your page to the tabbar

So far, you added a .vue file but the web app do not "knows" about it. The newly created .vue file must be [imported](https://vuejs.org/v2/guide/single-file-components.html#Introduction). 

Let's import this component where it belongs : in AppTabbar.vue.

* Open AppTabbar.vue like a pro \(using Ctrl-P\)

From the source below \(extracted from AppTabbar\), **figure out the syntax for importing your newly created page.**  

{% code title="AppTabbar.vue" %}
```javascript
import Pusher from "pusher-js";
import Map from "./pages/Map.vue";
import Home from "./pages/Home.vue";
import Profile from "./pages/Profile.vue";
import Arboretum from "./pages/Arboretum.vue";
import Releve from "./pages/Releves.vue";
import Folia from "./pages/Folia.vue";

```
{% endcode %}

Actually type the import line and save. 

{% hint style="info" %}
**Any file modification** triggers a reload of the application in development mode

This is very convenient : it permits to know exactly when a change breaks the app.
{% endhint %}

Your new page isn't yet in the tabbar. To make it happen, you need to change the value of the `tabs()` function. 

This function returns an array of objects, **each element of the array represent an item in the tabbar**.

```javascript
  tabs() {
      var tab = 
      [
        {
          label: this.$t('map'),
          icon: "ion-map",
          active: false,
          page: Map,
          theme: red
        },
        {
          label: this.$t('mission'),
          icon: "ion-home",
          page: Home,
          theme: red
        },       
     // ....
        {
          label: "Folia",
          icon: "ion-search",
          page: Folia,
          theme: purple
        }
      ];
      // .....
      return tab
    },
```

Taking inspiration from the last item of the array \(Folia\), add a new object defining your page to the array. This object will have three properties :

* `icon type String`
* `label type String` 
* `page type Object`

{% hint style="info" %}
To find a correct icon property value, find the desired icon in [ioniconics](https://ionicons.com/). Then append "ion-" to the icon name. \([ref](https://onsen.io/v2/api/vue/v-ons-icon.html)\)
{% endhint %}

You should now have a new tab entry leading to your newly created page. 

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

The `text` variable is here declared and initialized. It is now possible to refer to `text` in the UI. 

