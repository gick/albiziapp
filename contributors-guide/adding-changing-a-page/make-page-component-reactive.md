# Make page component reactive



## About reactivity 

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

## Practical example : mutating data

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

## Handling events to mutate data





