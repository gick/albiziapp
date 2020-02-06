# Optional challenge : make it prettier

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



