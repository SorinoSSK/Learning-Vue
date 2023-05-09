# Learning Vue

This repository contain a learning guide for me to pick up on vue.js. References of the content can be found at the very end of this repository. 

## Setting up Vue
**1)  Install Node.js**  
**2)  Create a vue project**  
```sh
npm init vue@latest
```
**3)  Answer the prompt**  
```
Vue.js - The Progressive JavaScript Framework

√ Project name: ... Test
√ Package name: ... test
√ Add TypeScript? ... No / Yes
√ Add JSX Support? ... No / Yes
√ Add Vue Router for Single Page Application development? ... No / Yes
√ Add Pinia for state management? ... No / Yes
√ Add Vitest for Unit Testing? ... No / Yes
√ Add an End-to-End Testing Solution? » No
? Add ESLint for code quality? » No / Yes
```
**4)  Install the project**  
```sh
npm install
```
**5)  Compile and local host**  
```sh
npm run dev
```
## Compile and Minify for Production
```sh
npm run build
```
## Ideology/Terminology behind Vue
### Mount
```test``` is the id of a division and mounting to ```#test``` will allow the manipulation of data by creating an object of variables.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            {{val}}
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: 'This is a test.'
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### `v-model`
```v-model``` is a component used in vue to bind values to variables.  
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            {{val}}
            <input v-model="val"/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: 'This is a test.'
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### `v-if`
```v-if``` is a conditional rendering and will render if the variable it is bounded to is true. Unlike ```v-show```, if ```v-if``` is given a false, the html component with ```v-if``` will not be loaded at all.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <div v-if="val">message</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### `v-else-if`, `v-else`
An addon to v-if.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
            v-cloak {
                display: none;
            }
        </style>
    </head>
    <body>
        <div id = "test" v-cloak>
            <div v-if="val">message</div>
            <div v-else-if="val2">message2</div>
            <div v-else>message3</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: false,
                        val2: true
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
However, you will notice that all components of ```v-if```, ```v-else-if```, and ```v-else``` will be rendered initially. To force vue to render only after the completion of if else, we can use ```v-cloak```.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <div v-if="val">message</div>
            <div v-else-if="val2">message2</div>
            <div v-else>message3</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: false,
                        val2: true
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### `v-show`
```v-show``` is almost similar to ```v-if```. However, instead of a conditional rendering, it is a conditional display. If ```v-show``` is given a false, the html will still be rendered but it's visibility will be set to false.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div>
        </div id = "test">
            <div v-show="val">message</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### `v-on`
```v-on``` is an event handler similar onClick(). The example below will show ```v-on``` **set to manage click events** and perform certain instructions. 
#### `v-on:click`
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <button v-on:click="val = true">Show "message"</button>
            <div v-if="val">message</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: false
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
We can set it to toggle by replacing ```v-on:click="val = true"``` to ```v-on:click="val = !val"```  
The code below works the same as the ones above.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <button @click="val = true">Show "message"</button>
            <div v-if="val">message</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: false
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
To increase the functionality of the event handler, we can set it to reference a method instead.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <button @click="afunction">Show "message"</button>
            <div v-if="val">message</div>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: false
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
#### `v-on:keyup`
The example below will set ```v-on``` to **manage keyboard events**.
```
<!DOCTYPE html>
<html>
    <head/>
    <body>
        <div id = "test">
            <button @click="afunction">Show "message"</button>
            <div v-if="val">message</div>
            <input @keyup.enter="inputMethod" v-modal = "val2">
            <!--The input below will be binded to key number 13 on the keyboard.--> 
            <input @keyup.13="inputMethod2(val2)">
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
``` 
You may concatenate input with some other string. For instance, we can change
```
<input @keyup.13="inputMethod2(val2)">
```
to the following
```
<input @keyup.13="inputMethod2(val2 + ' A TEST.')">
```
#### `v-on:submit`
This is a follow up on [Custom components](#custom-components). The function allows user to perform operation such as post. If ```@submit``` is used without ```@submit.prevent```, the webpage will have the refresh effect.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <h1>{{title}}</h1>
                        <input type = "email" v-model="email"/>
                        <input type = "password" v-model="password"/>
                        <button>Login</button>
                    </form>
                `,
                data() {
                    return {
                        title: 'A Form',
                        email: '',
                        password: ''
                    }
                },
                methods: {
                    handleSubmit() {
                        console.log(this.email, this.password)
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```

### Custom components
Create custom components. Custom components can be styled by using   ```<style></style>```.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.component('custom-form', {
                someForm: `
                    <div>
                        <h1>{{title}}</h1>
                        <input type = "email"/>
                        <input type = "password"/> 
                    </div>
                `,
                data() {
                    return {
                        title: 'A Form'
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
### Calling components within a component
We can call a component within a component by declaring using ```components``` and feeding it with an array of component we intend to use. ```components: ['custom-input']```
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <h1>{{title}}</h1>
                        <custom-input type = "email" v-model="email"/>
                        <custom-input type = "password" v-model="password"/>
                        <button>Login</button>
                    </form>
                `,
                components:['custom-input']
                data() {
                    return {
                        title: 'A Form',
                        email: '',
                        password: ''
                    }
                },
                methods: {
                    handleSubmit() {
                        console.log(this.email, this.password)
                    }
                }
            })
            app.component('custom-input', {
                template:
                    <label>
                        {{ label }}
                        <input type="text"/>
                    </label>
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
We could also pass data from one component to another component using ***v-bind***. For the sub component to accept the variable, ```props``` will have to be declared. For short notation, we can use ```:``` instead of ```v-bind:```.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <h1>{{title}}</h1>
                        <custom-input type = "email" v-bind:label="emailLabel"/>
                        <custom-input type = "password" v-bind:label="passwordLabel"/>
                        <button>Login</button>
                    </form>
                `,
                components:['custom-input']
                data() {
                    return {
                        title: 'A Form',
                        email: '',
                        password: '',
                        emailLabel: 'Email: ',
                        passwordLabel: 'Password: '
                    }
                },
                methods: {
                    handleSubmit() {
                        console.log(this.email, this.password)
                    }
                }
            })
            app.component('custom-input', {
                template: `
                    <label>
                        {{ label }}
                        <input type="text" v-model="value"/>
                    </label>
                `,
                props: ['label'],
                data() {
                    return {
                        value: ''
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```
However, the reverse will be a little complicated. To retrieve data from the child, we can use ```computed```. ```Get``` will retrieve value from parent component and ```Set``` will be used to retrieve from the child component. ```v-model``` contains a child property of ```modelValue```, thus we could retrieve value of ```v-modal``` by declaring the parameter ```modelValue``` in props.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data:function() {
                    return {
                        val: true,
                        val2: 'message'
                    }
                },
                methods: {
                    afunction() {
                        this.val = !this.val
                    },
                    inputMethod() {
                        console.log(this.val2)
                    },
                    inputMethod2(val2) {
                        console.log(val2)
                    }
                }
            })
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <h1>{{title}}</h1>
                        <custom-input type = "email" v-bind:label="emailLabel" v-model="email"/>
                        <custom-input type = "password" v-bind:label="passwordLabel" v-model="password"/>
                        <button>Login</button>
                    </form>
                `,
                components:['custom-input']
                data() {
                    return {
                        title: 'A Form',
                        email: '',
                        password: '',
                        emailLabel: 'Email: ',
                        passwordLabel: 'Password: '
                    }
                },
                methods: {
                    handleSubmit() {
                        console.log(this.email, this.password)
                    }
                }
            })
            app.component('custom-input', {
                template: `
                    <label>
                        {{ label }}
                        <input type="text" v-model="value"/>
                    </label>
                `,
                props: ['label', 'modelValue'],
                computed: {
                    value: {
                        get() {
                            return this.modelValue
                        },
                        set(values) {
                            this.$emit('update:modelValue, values') 
                        }
                    }
                }
                data() {
                    return {
                        value: ''
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html>
```

### Looping , `v-for`
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({})
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <h1>{{title}}</h1>
                        <p v-for="str in inputs" v-bind:key="str">{{str}}</p>
                        <p v-for="(str, i) in inputs" v-bind:key="i">{{i}}</p>

                    </form>
                `,
                components:['custom-input']
                data() {
                    return {
                        title: 'A Form',
                        inputs:[
                            'email',
                            'password',
                            'name'
                        ]
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html> 
```
### Looping through components
We can use for loop when we have multiple entries of the same component.
```
<!DOCTYPE html>
<html>
    <head>
        <style>
        </style>
    </head>
    <body>
        <div id = "test">
            <custom-form/>
        </div>
        <script src="https://unpkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({})
            app.component('custom-form', {
                someForm: `
                    <form @submit.prevent="handleSubmit">
                        <custom-input v-for="(input, i) in inputs" :key="i" v-model="input.value" :label="input.label" type="input.type"
                        <button>Login</button>
                    </form>
                `,
                components:['custom-input']
                data() {
                    return {
                        title: 'A Form',
                        inputs:[
                            {
                                label: 'Email',
                                value: '',
                                type: 'email'
                            },
                                                        {
                                label: 'Password',
                                value: '',
                                type: 'password'
                            },
                        ],
                        email: '',
                        password: '',
                        emailLabel: 'Email: ',
                        passwordLabel: 'Password: '
                    }
                },
                methods: {
                    handleSubmit() {
                        console.log(this.inputs[0].value, this.inputs[1].value)
                    }
                }
            })
            app.component('custom-input', {
                template: `
                    <label>
                        {{ label }}
                        <input :type="text" v-model="value"/>
                    </label>
                `,
                props: ['label', 'type', 'modelValue'],
                computed: {
                    value: {
                        get() {
                            return this.modelValue
                        },
                        set(values) {
                            this.$emit('update:modelValue, values') 
                        }
                    }
                }
                data() {
                    return {
                        value: ''
                    }
                }
            })
            app.mount('#test')
        </script>
    </body>
</html> 
```
### Lifecycle Hooks
Lifecycle Hooks performs similarly to actions such as on-mouseClick and on-mouseRelease. However, the difference is that Lifecycle hooks trigger events for components that is entering and leaving the DOM or when it is being removed from the system. The work flow of the lifecycle hooks can be found [here](https://vuejs.org/guide/essentials/lifecycle.html).
```
<!DOCTYPE html>
<html>
    <head>
        <title>Test</title>
        <style>
            .box {
                background-color:black;
                height:100px;
                width:100px;
            }
        </style>
    </head>
    <body>
        <div id = "app">
            <button @click="toggleBox">Toggle Box</botton>
            <test-box v-if="isVisible"/>
        </div>
        <script src="https://upkg.com/vue@next"/>
        <script>
            let app = Vue.createApp({
                data: function() {
                    return {
                        isVisible: false
                    }
                },
                methods:{
                    toggleBox: function() {
                        this.isVisible = !this.isVisible
                    }
                }
            })
            app.component('test-box', {
                template: `
                    <div class="box"/>
                `,
                created() {
                    console.log("created")
                },
                mounted() {
                    console.log("mounted")
                },
                unmounted() {
                    console.log("unmounted")
                }
            })
            app.mount('@app')
        </script>
    </body>
</html>
```

### Bootstrap
Add the following code for main.js
```
import "boostrap/dist/css/bootstrap.css"
import Vue from "vue"
import App from "./App.vue"

Vue.config.productionTip = false

new Vue({
    render: h => h(App),
})
.$mount('#app')

import "bootstrap/dist/js/bootstrap.js"
```


### Reference
- https://vuejs.org/guide/quick-start.html#creating-a-vue-application [Date of Access: 28/04/2023]
- https://www.youtube.com/watch?v=FXpIoQ_rT_c&t=85s [Date of Access: 28/04/2023]
- https://www.youtube.com/watch?v=oZ9zlS5V5WU [Date of Access: 09/05/2023]