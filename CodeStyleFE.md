# Code style

### NAMING

#### Multi-word component names
Component names should always be multi-word, except for root App components, and built-in components provided by Vue, such as <transition> or <component>.
```js
// ----------- bad
components/
    |- Todo.vue

// ----------- good
components/
    |- TodoItem.vue
```
<br>

#### Base component names
Base components (a.k.a. presentational, dumb, or pure components) that apply app-specific styling and conventions should all begin with a specific prefix, such as Base.
<br><br>

#### Single-instance component names
Components that should only ever have a single active instance should begin with the The prefix, to denote that there can be only one.
```js
// ----------- bad
components/
    |- Header.vue
    |- MySidebar.vue

// ----------- good
components/
    |- TheHeader.vue
    |- TheSidebar.vue
```
<br>

#### Tightly coupled component names
Child components that are tightly coupled with their parent should include the parent component name as a prefix.
```js
// ----------- bad
components/
    |- Gallery.vue
    |- Feedbacks.vue
    |- Team.vue
    |- Text.vue

// ----------- good
components/
    |- HomeGallery.vue
    |- HomeFeedbacks.vue
    |- AboutTeam.vue
    |- AboutText.vue
```
<br>

Predicate(returns boolean) functions/variables names always start with `is` or `has`
```js
// ----------- bad
const odd => (num) {
    return num % 2;
}
    
const pets = ['cat', 'dog', 'bat'];
const cat => (str) {
    return pets.includes(str)
} 


// ----------- good
const isOdd => (num) {
    return num % 2;
}
   
const pets = ['cat', 'dog', 'bat'];
const hasCat => (str) {
    return pets.includes(str)
} 
```
<br>

If function get data from API and does not return anything, name always start with `fetch`
```js
// ----------- bad
getTickets() {
  tickets = await api.tickets.getTickets();
}

// ----------- good
fetchTickets() {
  tickets = await api.tickets.getTickets();
}
```
<br>

If function return some data, name always start with `get`
```js
// ----------- bad
getTickets() {
  tickets = [...];
}
getTickets() {
  tickets = await api.tickets.getTickets();
}

// ----------- good
getTickets() {
  tickets = [...];
  return tickets;
}
```
<br>

If function has arguments and does not return anything, name always start with `set`
```js
// ----------- bad
setTickets() {
  newTickets = [...];
}

// ----------- good
setTickets(tickets) {
  newTickets = tickets;
}
```
<br>

#### Lists naming      
Lists always plural names
```js
// ----------- bad
const children = node.childNodes;

// ----------- good
const childrens = node.childNodes;
```

Counts always plural names and ends with `Count`
```js
// ----------- bad
const children = node.childNodes.length;
const childrens = node.childNodes.length;
const childrenCount = node.childNodes.length;

// ----------- good
const childrensCount = node.childNodes.length;
```
<br>

#### The names of the emitted events are written in the camelCase
```js
// ----------- bad
<template>
    <tag @click="$emit('some-event')" />
</template>

// ----------- good
<template>
    <tag @click="$emit('someEvent')" />
</template>
```

<br><br>

### CSS

#### Using a scss mixin without argument is written without parentheses
```js
// ----------- bad
<style>
.class {
    @include content();
}
</style>

// ----------- good
<style>
.class {
    @include content;
}
</style>
```
<br>

#### Use ::v-deep + scoped styles to customize custom vuetify components
```js
// ----------- bad
<style>
.class .v-input__icon--append .v-icon {
    color: var(--red) !important;
}
</style>

// ----------- good
<style scoped>
.class::v-deep .v-input__icon--append .v-icon {
    color: var(--red) !important;
}
</style>
``` 
<br>

#### Do not mix custom tag classes and vuetify etc. library classes
```js
// ----------- bad
<tag class="header__logo my-1 d-flex" />

// ----------- good
<tag class="header__logo" />
or
<tag class="my-1 d-flex" />
```
<br>

#### Colors are defined only as global variables (do not hardcoded colors in templates or styles)

```js
// ----------- bad
<template>
    <tag color="primary" />
    <tag color="#fffff" />
</template>

<style>
.class {
    color: red;
    background-color: #0000;
}
</style>

// ----------- good
<template>
    <tag color="var(--black)" />
</template>

<style>
.class {
    color: var(--red);
    background-color: var(--green);
}
</style>
```

<br><br>
    
### GLOBAL
#### All components on the same nesting level
```js
// ----------- bad
components/
    Home/
        |- HomeGallery.vue
        |- HomeFeedbacks.vue
    About/
        |- AboutTeam.vue
        |- AboutText.vue

// ----------- good
components/
    |- HomeGallery.vue
    |- HomeFeedbacks.vue
    |- AboutTeam.vue
    |- AboutText.vue
```
<br>

#### Component data should not be an arrow function
```js
// ----------- bad
 data: () => ({
    foo: 'bar'
 })

// ----------- good
 data() {
     return {
         foo: 'bar'
     }
 }
```
<br>

#### Don't leave empty sections
```js
// ----------- bad
<script></script>
<style></style>
```
<br>

#### Add type and required to props
```js
// ----------- bad
props: ['status']

// ----------- good
props: {
  status: {
    type: String,
    required: false,
    default: ''
  }
}
```
<br>

#### Self-closing components
```js
// ----------- bad
<MyComponent></MyComponent>

// ----------- good
<MyComponent/>
```
<br>

#### Component options order
- imports
- name
- components
- filters
- extands
- mixins
- props
- data
- computed
- watch
- beforeCreate
- created
- beforeMount
- mounted
- beforeUpdate
- updated
- activated
- deactivated
- beforeDestroy
- destroyed
- methods
<br><br>

#### Always add a TODO for the temporary code
```js
// TODO: rename component
<MyComponent/>
```    
<br>

#### Don't use computed property for `v-model`
```js
// ----------- bad
<templage>
    <v-checkbox v-model="isShowChip">
        ...
    </v-checkbox>
</templage>
<script>
    computed: {
        isShowChip: {
          get() { ... },
          set(value) { ... }
        }
    }
</script>

// ----------- good
<templage>
    <v-checkbox v-model="isShowChip">
        ...
    </v-checkbox>
</templage>
<script>
    data: () {
        return {
            isShowChip: false
        }
    },
    watch: {
        isShowChip(value) { ... }
    }
</script>
```
<br>

#### Don't create a method for one line code
```js
// ----------- bad
<templage>
    <div @click="showModal">Show modal</div>
</templage>
<script>
    methods: {
        showModal () {
            this.isShowModal = true
        }
    }
</script>

// ----------- good
<templage>
    <div @click="isShowModal = true">Show modal</div>
</templage>
```   
    
<br>

#### Always add comment with example of result format data if it is not clearly enough, especially for regEx
```js
// ----------- good
getDate() {
    // MM/DD/YYYY
    return date.substring(0, 10)
}
    
getFormatedDate(date) {
    // MM/DD/YYYY
    const pattern = /(0[1-9]|1[012])[- /.](0[1-9]|[12][0-9]|3[01])[- /.](19|20)\d\d/
    return pattern.test(value)
}
```   
