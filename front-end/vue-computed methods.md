Notes about computed methods in Vue.js

Usually, computed methods in [Vue.js](https://vuejs.org/)
are always considered as way to generate data for rendering.

One example is
```HTML
<template>
  <ul>
    <li v-for="(item, index) in items" :key="index"> <!-- Notice the items here! -->
        {{do something here}}
    </li>
  </ul>
</template>

<script>
export default {
    name:"You name it",
    data() {
      return {
      // Notice nothing here
      }
    },
    computed:{
      items(){ // here is where the items come from !
        return [
          {
              data:"item 1"
          },
          {
              data:"item 2"
          },
          {
              data:"item 3"
          },
        ]
      }
    }
}
</script>
```
but some times we need to deal with nested structural data object like:
```JSON
  {
    "children": {
      "grandsons": [
        {"gs1": "data"},
        {"gs2": "data"},
        {"gs3": "data"},
        ...
      ]  
    },
    "child": {
      "property1":"p1",
      "property2":"p2",
      "property3":"p3",
      ...
    },
    ...
  }
```

It is very annoying to write bunches of "SomethingA.SomethingB.Somewhat.bla.bla" stuff in your code 
<strong>and may cause difficulty in reading your code</strong>, so one way to mitigate this is to use computed methods.

for the above example data you can just break it into computed methods:
```HTML

<template>
  <ul>
    <li v-for="(item, index) in grandsons" :key="index"> <!-- Notice the grandsons here! -->
        {{do something here}}
    </li>
  </ul>
</template>
<script>
//...
export default {
//...
    data() {
      return {
        data: **example data as above**
      }
    },
    computed: {
        children() {
          return this.data.children; // Do not forget "this" !
        },
        grandsons() {
          return this.children.grandsons; // simple reference from the parent object, hoho
        },
        child() {
          return this.data.child; 
        }
    }
}
</script>
```
Things seem to be much more clear right? But there are good news about computed methods: <strong>they are two way binded!</strong>
You can use them as they are just the object/data themselves!

```JavaScript
methods: {
    changeChild(value){
        this.child = value; // I believe this is the magic of Vue.js. Further investigation needed :)
    }
}

```
Thank you for your time!
