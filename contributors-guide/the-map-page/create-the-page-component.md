# Create the page component

Start Albiziapp locally \(you might have to kill already running albiziapp processes\)

{% hint style="info" %}
Use`vue ui`from the albiziapp/ directory then Task`->`Serve`->`Run task 
{% endhint %}

This action triggers the source dependencies injection, their bundling and then start serving Albiziapp at [http://localhost:8080/](http://localhost:8080/)

![Expected output at http://localhost:8000/](../../.gitbook/assets/image%20%281%29.png)

{% hint style="info" %}
From vue-dashboard on top left menu : "open in editor" . It should open VSCode.
{% endhint %}

* Create a .vue file in the pages directory. **The file should start with a capital case**.

This file is first empty. Let's fill it a bit :

{% hint style="info" %}
Use Ctrl-Space to trigger the powerful autocomplete. Chose the first option
{% endhint %}

![](../../.gitbook/assets/image%20%286%29.png)

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

### 

