# Creating a new page \(exercise\)

## Objectives

To create a new page, accessible from the navbar with a given icon

 The page will displays in real time the total number of observation. 

A new observation from another user should be reflected immediately in the counter. A new observation from the current user should update the counter.

## Steps to follow

### The easy steps

* Start Albiziapp locally 

{% hint style="info" %}
Use`vue ui`from the albiziapp/ directory then Task-&gt;Server-&gt;Run task 
{% endhint %}

![Expected output](../.gitbook/assets/image%20%281%29.png)

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

Using autocomplete, populate the template. Add the v-ons-page element as direct child of template. Then add something to display for test purposes.

```javascript
<template>
  <v-ons-page>
      <div>Hello page</div>
  </v-ons-page>
</template>
```

### Less easy steps

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

Your new page isn't yet in the tabbar. To make it happen, you need to change the value of the `tabs()` function. This function is 



### Step 1 to 3



