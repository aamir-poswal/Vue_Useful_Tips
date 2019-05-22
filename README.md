### Vue.js-Watch for nested Data

For individual property
```javascript
var vm = new Vue({
    data: {
        customer: {
            firstName: 'John',
            lastName: 'Doe',
        }
    },
    watch: {
        'customer.firstName': function (newVal, oldVal) {
            //to work with changes in someOtherProp
        },
        'customer.lastName': function (newVal, oldVal) {
            //to work with changes in prop
        }
    },
})
```

### Watch on entire object using deep option

vm.someObject.nestedValue = 123 // callback is fired

```javascript
var vm = new Vue({
    data: {
        customer: {
            firstName: 'John',
            lastName: 'Doe',
        }
    },
    watch: {
        vm.$watch('customer', callback, {
            deep: true
        })
    },
})
```

### Vue.js- Delay in Watch function

I used lodash _.debounce to achieve following.

```javascript

    'grvSearchModel':_.debounce(function (newVal) {
      if(newVal&& !_.isEmpty(newVal)){
          this.grvLines=[]
        }
    }, 50),

```

### Vue.js- Delay in vue computed function 

using lodash _.debounce
```javascript
computed:{
    aircraftCategories:{
        get () {
          return this.$store.state.mro.capability.aircraftCategories
        },
        set: _.debounce(function (v) {
          this.$store.dispatch('mro/saveSection', {section: 'capabilities',key:'aircraftCategories',value: v})
        }, 1000)
    },
}
```

### Vue.js- Changing the selected option of an HTML Select element

```javascript
<div id="app">
    <select v-model="val">
        <option value="1">Cat</option>
        <option value="2">Dog</option>
        <option value="3">Fish</option>
    </select>
</div>
<script>
    var app = new Vue({
        el: '#app',
        data: {
                val: null,
        },
        mounted: function() {
                this.val = 3;
        }
    });
</script>
```

### Vue.js- How do I hide the VueJS syntax while the page is loading?

You can use v-clock
```javascript
<div v-cloak>{{ message }}</div>
```
### Vue.js- How to call multiple function with v-on:click
```javascript
<div v-on:click="firstFunction(); secondFunction();"></div>
```
### Vue.js- display unescaped html

You can use v-html

```javascript
<div v-html="htmlContent"></div>
```
### Vue.js- Mouseover or hover 

```javascript
<div id="demo">
        <div v-show="active">Show</div>
        <div @mouseover="mouseOver">Hover over me!</div>
    </div>

var demo = new Vue({
    el: '#demo',
    data: {
        active: false
    },
    methods: {
        mouseOver: function(){
            this.active = !this.active;   
        }
    }
});
```
### Vue.js- image source concatenate variable and text
```javascript
<img v-bind:src="imagebaseUrl + 'images/logo.png'">
```
Using template literal ES6 with backticks
```javascript
<img v-bind:src="`${ imagebaseUrl }'images/logo.png`">
```
### Vue.js- call a vue.js function on page load

You can call this function in beforeMount section of a Vue component: like following:
```javascript
....
 methods:{
     getUnits: function() {...}
 },
 beforeMount(){
    this.getUnits()
 },
 ......
```

### Vue.js update parent data from child component

One option is to use store vuex
```javascript
Vue.component('child', {
  template: '#child',
  
  //The child has a prop named 'value'. v-model will automatically bind to this prop
  props: ['value'],
  methods: {
    updateValue: function (value) {
      this.$emit('input', value);
    }
  }
});

new Vue({
  el: '#app',
  data: {
    parentValue: 'hello'
  }
});

<script src="https://cdnjs.cloudflare.com/ajax/libs/vue/2.5.13/vue.js"></script>

<div id="app">
  <p>Parent value: {{parentValue}}</p>
  <child v-model="parentValue"></child>
</div>

<template id="child">
   <input type="text" v-bind:value="value" v-on:input="updateValue($event.target.value)">
</template>
```

### Vue.js how to watch store values from vuex

```javascript
<template>
  <!-- We meet our first objective (1) by simply -->
  <!-- binding to the count property. -->
  <p>Fruits: {{ count }}</p>
</template>

<script>
import basket from '../resources/fruit-basket'

export default () {
  computed: {
    count () {
      return basket.state.fruits.length
      // Or return basket.getters.fruitsCount
      // (depends on your design decisions).
    }
  },
  watch: {
    count (newCount, oldCount) {
      // Our fancy notification (2).
      console.log(`We have ${newCount} fruits now, yaay!`)
    }
  }
}
</script>
```


