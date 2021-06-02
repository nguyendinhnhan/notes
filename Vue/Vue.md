### Lifecycle

![alt text](./images/lifecycle.svg)

Template syntax

    <span>Message: {{ msg }}</span>
    <span v-once>This will never change: {{ msg }}</span>

    <p>Using mustaches: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>
    Using mustaches: <span style="color: red">This should be red.</span>;
    Using v-html directive: This should be red.

    <div v-bind:id="'list-' + id"></div>

```
v-bind:attr     - v-bind:id, v-bind:class, v-bind:href,...
v-on:event      - v-on:click
```

Dynamic Arg
```
v-bind:[attributeName]
v-on:[eventName]
```

Modifiers
```html
<form v-on:submit.prevent="onSubmit">...</form>
the .prevent modifier tells the v-on directive to call event.preventDefault() on the triggered event
```

Shorthands
```html
    <!-- full syntax -->
    <a v-bind:href="url"> ... </a>

    <!-- shorthand -->
    <a :href="url"> ... </a>

    <!-- shorthand with dynamic argument -->
    <a :[key]="url"> ... </a>
```
```html
    <!-- full syntax -->
    <a v-on:click="doSomething"> ... </a>

    <!-- shorthand -->
    <a @click="doSomething"> ... </a>

    <!-- shorthand with dynamic argument -->
    <a @[event]="doSomething"> ... </a>
```

```javascript
    // in component
    methods: {
        calculateBooksMessage() {
            return this.author.books.length > 0 ? 'Yes' : 'No'
        }
    }
    'computed' properties are cached based on their reactive dependencies -> should use computed

    should use 'computed' rather than 'watch'

    const app = Vue.createApp({
        data() {
            return { 
                author: {
                    name: 'John Doe',
                    books: [
                        'Vue 2 - Advanced Guide',
                        'Vue 3 - Basic Guide',
                        'Vue 4 - The Mystery'
                    ]
                } 
            }
        },
        methods: {
            click() {
                // ... respond to click ...
            }
        },
        created() {
            // Debouncing with Lodash
            this.debouncedClick = _.debounce(this.click, 500)
        },
        computed: {
            // a computed getter
            publishedBooksMessage() {
                // `this` points to the vm instance
                return this.author.books.length > 0 ? 'Yes' : 'No'
            }
        },
        watch: {
            // whenever name changes, this function will run
            name(newName, oldName) {}
        },
        unmounted() {},
        template: `
            <button @click="debouncedClick">
            Save
            </button>
        `
    })
```

Class and style bindings
```html
    <div :class="{ active: isActive }"></div>

    <div :class="[activeClass, errorClass]"></div>  
```
```javascript
    data() {
        return {
            activeClass: 'active',
            errorClass: 'text-danger'
        }
    }
```