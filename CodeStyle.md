# Code style

### Colors are defined only as global variables (do not hardcoded colors in templates or styles)

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

### Using a scss mixin without argument is written without parentheses
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

### The names of the emitted events are written in the camelCase
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

### All components on the same nesting level
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

### Naming
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

#### Base component names
Base components (a.k.a. presentational, dumb, or pure components) that apply app-specific styling and conventions should all begin with a specific prefix, such as Base.

#### Single-instance component names
Components that should only ever have a single active instance should begin with the The prefix, to denote that there can be only one.
```js
// ----------- bad
components/
    |- Heading.vue
    |- MySidebar.vue

// ----------- good
components/
    |- TheHeading.vue
    |- TheSidebar.vue
```
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
    
#### Predicates naming
Predicates names always start with is
```js
// ----------- bad
const admin = true;
setAdmin(true);
getAdmin() => {
    return true;
}

// ----------- good
const isAdmin = true;
setIsAdmin(true);
getIsAdmin() => {
    return true;
}
```
    
Entries predicates names always start with has
```js
// ----------- bad
node.children();
children(node);

// ----------- good
node.hasChildren();
hasChildren(node);
```
    
#### Lists naming      
Lists always plural names
```js
// ----------- bad
const children = node.childNodes;

// ----------- good
const childrens = node.childNodes;
```

Counts always plural names and ends with Count
```js
// ----------- bad
const children = node.childNodes.length;
const childrens = node.childNodes.length;
const childrenCount = node.childNodes.length;

// ----------- good
const childrensCount = node.childNodes.length;
```


### Component data should not be an arrow function
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

### Don't leave empty sections
```js
// ----------- bad
<script></script>
<style></style>
```

### Add type and required to props
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

### Self-closing components
```js
// ----------- bad
<MyComponent></MyComponent>

// ----------- good
<MyComponent/>
```

### Component options order
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

### Always add a TODO for the temporary code
```js
// TODO: rename component
<MyComponent/>
```

### Do not mix custom tag classes and vuetify etc. library classes
```js
// ----------- bad
<tag class="header__logo my-1 d-flex" />

// ----------- good
<tag class="header__logo" />
or
<tag class="my-1 d-flex" />
```

### Use ::v-deep + scoped styles to customize custom vuetify components
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
