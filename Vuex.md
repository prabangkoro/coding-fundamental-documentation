# **Vuex Documentation**

## **State**

Vuex uses a single state tree - that is, this single object contains all your application level state and serves as the "single source of truth". This also means usually you will have only one store for each application. A single state tree makes it straightforward to locate a specific piece of state, and allows us to easily take snapshots of the current app state for debugging purposes.

Note:
Vuex state gives you a simple way to store a global, a trusted data that you can access and modify everywhere.

### **Getting Vuex State into Vue Components**

How to use it right away (see code below). Simply call **state** inside **store**.

```js
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return store.state.count
    }
  }
}
```

You can also inject store from Vue component declaration to the component child.

```js
const app = new Vue({
  el: '#app',
  // provide the store using the "store" option.
  // this will inject the store instance to all child components.
  store,
  components: { Counter },
  template: `
    <div class="app">
      <counter></counter>
    </div>
  `
})
```

And now you can use it by calling $store

```js
const Counter = {
  template: `<div>{{ count }}</div>`,
  computed: {
    count () {
      return this.$store.state.count
    }
  }
}
```

### **mapState Helper**

When you deal with multiple store state properties or getters, repeating these computed value of state can be verbose and repetitive. You can use **mapState** helper. mapState will generate you a getter function automatically!

```js
// in full builds helpers are exposed as Vuex.mapState
import { mapState } from 'vuex'

export default {
  // ...
  computed: mapState({
    // arrow functions can make the code very succinct!
    count: state => state.count,

    // passing the string value 'count' is same as `state => state.count`
    countAlias: 'count',

    // to access local state with `this`, a normal function must be used
    countPlusLocalState (state) {
      return state.count + this.localCount
    }
  })
}
```

Or you can also mention name of state in an array of string:

```js
computed: mapState([
  // map this.count to store.state.count
  'count'
])
```

#### **Object Spread Operator**

Note that mapState returns an object. How do we use it in combination with other local computed properties? Normally, we'd have to use a utility to merge multiple objects into one so that we can pass the final object to computed. However with the object spread operator (which is a stage-4 ECMAScript proposal), we can greatly simplify the syntax:

```js
computed: {
  localComputed () { /* ... */ },
  // mix this into the outer object with the object spread operator
  ...mapState({
    // ...
  })
}
```

## **Getters**

For sharing a computed state of store value, we can use a Getters. Vuex allows us to define "getters" in the store. You can think of them as computed properties for stores. Like computed properties, a getter's result is cached based on its dependencies, and will only re-evaluate when some of its dependencies have changed.

Getters will receive the state as their 1st argument:

```js
const store = new Vuex.Store({
  state: {
    todos: [
      { id: 1, text: '...', done: true },
      { id: 2, text: '...', done: false }
    ]
  },
  getters: {
    doneTodos: state => {
      return state.todos.filter(todo => todo.done)
    }
  }
})
```

### **Property-Style Access**

If you want to access the value of a getters properties right away, you can access it like a normal property. The getters will be exposed on the store.getters object, and you access values as properties:

```js
store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]
```

Getters will also receive other getters as the 2nd argument:

```js
getters: {
  // ...
  doneTodosCount: (state, getters) => {
    return getters.doneTodos.length
  }
}
```
```js
store.getters.doneTodosCount // -> 1
```
We can now easily make use of it inside any component:

```js
computed: {
  doneTodosCount () {
    return this.$store.getters.doneTodosCount
  }
}
```

### **Method-Style Access**

If you want to pass an argument to the getter propertie, you can define the getters properties like a method. You can also pass arguments to getters by returning a function. This is particularly useful when you want to query an array in the store:

```js
getters: {
  // ...
  getTodoById: (state) => (id) => {
    return state.todos.find(todo => todo.id === id)
  }
}
```
```js
store.getters.getTodoById(2) // -> { id: 2, text: '...', done: false }
```
Note that getters accessed via **methods** will run each time you call them, and the result is **not cached**.

### The mapGetters Helper

Simply get any Getters using mapGetters by passing array of getters name.

```js
import { mapGetters } from 'vuex'

export default {
  // ...
  computed: {
    // mix the getters into computed with object spread operator
    ...mapGetters([
      'doneTodosCount',
      'anotherGetter',
      // ...
    ])
  }
}
```
To use a different name, use an object
```js
...mapGetters({
  // map `this.doneCount` to `this.$store.getters.doneTodosCount`
  doneCount: 'doneTodosCount'
}
```


