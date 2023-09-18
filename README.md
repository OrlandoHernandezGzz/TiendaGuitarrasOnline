# Vue 3 + Vite

This template should help get you started developing with Vue 3 in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (and disable Vetur) + [TypeScript Vue Plugin (Volar)](https://marketplace.visualstudio.com/items?itemName=Vue.vscode-typescript-vue-plugin).


## Single File components.

Es basicamente el HTML, CSS y JS en un solo archivo.

¿Qué son los single file componentes?

Vue utiliza componentes para la creación de aplicaciones y sitios web.

Un componente debe tener la extensión .vue

Un componente usualmente tiene 2 propositos: ser reutilizable o separar la funcionalidad;
si se cumplen ambas es aún mejor.

Single File Components (SFC) es una convención en la cual un componente contiene 3 partes:
```js
    <script> <template> y <style>
```

## API Styles.

Es la forma en las que vas a escribir código.

Se tiene dos formas:

Options API está disponible desde Vue.js 2 mientras que Composition API desde la versión
2.7 y es la recomendada para proyectos con Vue 3.

- Options API

Con Options API se define la lógica de un componente utilizando una sintaxis de objeto.

Algunos Dev's con experiencia en lenguajes orientados a objetos encuetran esta forma más fácil de aprender.

```js 
    export default({
        components: {Productos },
        data() {
            return {
                productos: [],
                carrito: []
            }
        },
        mounted() {
            fetch('https://ecommerce.site/api')
                .then(res => res.json())
                .then(data => this.productos = data.data)
        },
        methods() {
            agregarCarrito(producto) {
                this.carrito.push(producto)
            }
        }
    })
```

- Composition API

Se definen los componentes utilizando Imports (tanto para funciones de Vue como librerías).

Se define Composition API añadiendo setup al script.

Composition API tiene 2 funciones para reactividad: reactive y ref.

Si tienes experiencia con React esta forma puede resultar familiar en muchas cosas.

```js
    import { ref } from 'vue'

    const productos = ref([])
    const carrito = ref([])

    const consultarAPI = () => {
        fetch('http://ecommerce.site/api')
            .then(res => res.json())
            .then(data => productos.value = data.data)
    }

    consultarAPI()

    const agregarCarrito(producto) => {
        carrito.value.push(producto)
    }
```

### ¿Cuál API utilizar?

Composition API permitirá tener código más reutilizable.

Options API es recomendado si tu proyecto utilizará pequeñas piezas de Vue o escenarios no tan complejos, también si prefieres el estilo orientado a objetos.

Composition API es recomendado si todo tu proyecto será hecho con Vue.js.


## State en Vue.js

Hay dos formas de manejar el state en composition API: Reactive y ref.

El state (o estado) determina la situación actual de nuestra aplicación.

Si un carrito de compras esta lleno o vacío, si un cliente aceptó un viaje o no, si un 
usuario esta autenticado o no; son ejemplos del estado de nuestra aplicación.

El state o estado no es siempre igual; tiende a cambiar en base a las interacciones
del usuario (clicks, formularios, navegar en diferentes páginas).

Debido a que el state tiende a cambiar; Vue.js tiene un par de funciones que nos
permitirán declararlo y sobretodo identificar cuando el state ha cambiado.

Estas 2 funciones son: ref y reactive; ambas se importan de vue.

Estas 2 funciones solo están dispionibles con Composition API.

Una vez que el state cambie el DOM de tu aplicación se actualizará.

### State con Reactive
Reactive siempre es un objeto.

```js
    import { reactive } from 'vue'

    const libro = reactive({
        disponible: true,
        nombre: 'Algoritmos 3',
        precio: 349,
        ISBN: "0-7533-1232-3"
    })

    // Para acceder a las propiedades.
    console.log(libro.disponible) // true
    console.log(libro.nombre) // Algoritmos 3
    console.log(libro.precio) // 349

    // Para modificar reactive:
    libro.disponible = false
    console.log(libro.disponible) // false
```


### State con Ref

Reactive es un objeto; que lo hace el ideal cuando quieres agrupar datos, 
¿Pero qué pasa con los arrays, booleans o strings?

Ref te permite trabajar con estos tipos de datos.

Cuando declaras un Ref deberás colocar su valor inicial.

```js
    import { ref } from 'vue'

    const clientes = ref([])
    const libro = ref({})
    const auth = ref(false)
    const mensaje = ref('Hola')

    // Acceder a las propiedades de ref:
    console.log(clientes.value) // Proxy
    console.log(auth.value) // false
    console.log(mensaje.value) // 'Hola'

    // Reescribir un ref
    clientes.value.push(nuevoCliente)
    auth.value = true
    mensaje.value = 'Nuevo texto'
```

En caso de necesitar evaluar diferentes valores se recomienda utilizar un 
computed property.



## Iterando sobre el state y que son las directivas de Vue js.

Las directivas en Vue js.

Son atributos HTML con ciertas funcionalidades de javascript.

Influenciadas por AngularJS las directivas de Vue.js es lo que llevan a este framework
a un nuevo nivel.

Las directivas en Vue js siempre inician con v- y se colocan como atributos HTML.

Directivas:

- v-text
- v-html
- v-show
- v-if
- v-else
- v-else-if
- v-for
- v-on
- v-bind
- v-model
- v-slot
- v-pre
- v-once
- v-memo
- v-cloak


## Creando componente en Vue js y pasando datos con props.

Los props sirven para comunicar componentes.

Vue js utiliza Props para pasar información entre componentes; estos props
pueden ser datos estáticos o reactivos.

En caso de querer pasar funciones se recomienda que sea por medio de un Component
Event.

Los Props nunca deben modificar el state en el componente hijo.


## Eventos en Vue js.

Todas las aplicaciones requieren ciertas interacciones por parte del usuario.

Presiontar un botón o link; llenar un formulario, son algunas de las acciones del DOM
más comunes.

Vue.js hace muy sencillo interactuar con ciertos eventos con la directiva v-on.

En vue js hay 2 tipos de eventos: Inline Handlers y Method Handlers.

Los inline son para tareas muy sencillas como cambiar a dark o light mode.

Los method Handlers son muy útiles cuando realizarás diferentes acciones como validar
los datos de un formulario.


## Component Events

@click y @submit son eventos muy comunes en nuestros proyectos,
debido a que el State de un proyecto no puede cambiarse en los Props lo ideal
es registrar un evento para el componente.

Por default un evento que se asocia a un botón o formulario buscará una
función en ese componente; pero para comunicarlo con el componente padre debemos
utilizar una sintaxis especial llamada emit y registrar un componente event o
evento del componente.

