# Bind the page component to the tabbar

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

