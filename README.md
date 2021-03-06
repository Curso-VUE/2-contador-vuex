# Aplicación contador con VueJS 2 + Vuex + Vue Cli 3

1. [Primer propyecto con Vue UI](#vueUI)
2. [Entendiendo un proyecto creado con Vue Cli](#vueCli)
3. [Introducción a Vuex](#vuex)
4. [Definir la tienda de datos con Vuex, state y mutations](#store)
5. [Componente Counter](#counter)
6. [Primera version del componente accediendo a Vuex](#vuex1)
7. [Segunda version del componente: mapState y mapMutations](#vuex2)

<hl>

<a name="vueUI"></a>

## 1. Primer proyecto con Vue UI

La interfaz de Vue UI se arranca con el comando ```vue ui```. Esto abrirá en el navegador la ruta http://localhost:8000 en donde se estará ejecutando la interfaz.

Esta interfaz permite administrar nuestros proyectos de vue y facilita la creación de nuevos proyectos especificando las librerías que van a utilizarse y configurando el punto de partida del proyecto.

En este caso vamos a configurar lo siguiente:
- Inicializar git
- Preset manual
  - Babel
  - Vuex
  - CSS preprocessor (Stylus)
  - Linter -> SI
  - Tests -> NO

Una vez creado el proyecto, desde esta interfaz podemos ejecutarlo en desarrollo o hacer el build.

<hl>

<a name="vueCli"></a>

## 2. Entendiendo un proyecto creado con Vue Cli

Primero eliminamos del proyecto el componente *HelloWorld.vue*. De *App.vue* debemos eliminar la importación, la carga en componentes y la renderización en el template de este componente.

El punto de entrada de nuestra aplicación es main.js. en el se realiza la instanciación del componente App que es el que contendrá todos los compoentes.

Cada componente tiene tres secciones diferenciadas:
- Template: Contiene el html.
- Script: Contiene las propiedades y métodos del componente, así como la declaración de los componentes hijos a los que se hace referencia en el template.
- Style: Contiene los distintos estilos css del componente. Podemos establecer que los estilos se apliquen únicamente al componente actual mediante el atributo scoped.

<hl>

<a name="vuex"></a>

## 3. Introducción a Vuex

Vuex permite manejar el estado centralizado de aplicaciones VueJS mediante el **store**.

![Vuex](./readme-images/vuex.png)

En el **store** nos encontramos con distintos elementos:
- state: Son los datos de nuestra aplicación.
- mutatuions: Realizan modificaciones sobre el estado.
- actions: Se utilizan para realizar peticiones asíncronas a otros servicios.

<hl>

<a name="store"></a>

## 4. Definir la tienda de datos con Vuex, state y mutations

Lo primero que hacemos es cargar el CDN de boostrap en el index.html de public. Posteriormente utilizaremos boostrap-vue.

En el archivo *index.js* de la carpeta *store* añadimos el estado **counter** y dos *mutations* para incrementar y decrementar el contador:

~~~js
export default new Vuex.Store({
  state: {
    counter: 0
  },
  mutations: {
    increment(state) {
      state.counter += 1
    },
    decrement(state) {
      state.counter -= 1
    }
  },
  actions: {
  },
  modules: {
  }
})
~~~

<hl>

<a name="counter"></a>

## 5. Componente counter

Creamos un nuevo componente *counter.vue*:

~~~html
<template>
  <div class="container">
    Hola desde counter
  </div>
</template>

<script>
export default {
  
}
</script>
~~~

Luego lo inportamos en el script del componente principal:

~~~html
<script>
import CounterCmp from "@/components/Counter";
export default {
  name: "App",
  components: {
    CounterCmp,
  },
  data() {
    return {
      text: "hola",
    };
  },
};
</script>
~~~

Y lo renderizamos en el template, usando una etiqueta en minúsculas y con guiones en lugar de CamelCase: 

~~~html
<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <p>{{ text }}</p>
    <counter-cmp></counter-cmp>
  </div>
</template>
~~~

<hl>

<a name="vuex1"></a>

## 6. Primera versión del componente accediendo a vuex

En el template del componente counter añadimos los elementos necesarios para el contador:

Para poder ver el estado de la variable counter hacemos referencia a ella con ```{{ $store.state.counter }}```.

Para añadir los eventos al click del botón utilizamos ```@click="$store.commit('nombre-del-mutation')```

~~~html
  <div class="container">
    <button
      class="btn btn-success btn-block"
      @click="$store.commit('increment')"
    >
      Incrementar
    </button>
    <div class="alert alert-secondary text-center mt-3">
      {{ $store.state.counter }}
    </div>
    <button
      class="btn btn-danger btn-block"
      @click="$store.commit('decrement')"
    >
      Decrementar
    </button>
~~~

<hl>

<a name="vue2"></a>

## 7. Segunda version del componente: mapState y mapMutations

Aunque la forma de trabajar con *$store.state* y *$store.commit* es prefectamente válida, vuex proporciona dos elementos para mapear el estado y los mutations y trabajar de forma más limplia.

En el script del componente declarams computed y methods de esta forma:

~~~html
<script>
import { mapState, mapMutations } from 'vuex'
export default {
  computed: {
    ...mapState(['counter']),
  },
  methods: {
    ...mapMutations(['increment', 'decrement'])
  }  
}
</script>
~~~

Y modificamos el template para acceder a los elementos del state mapeados:

~~~html
  <div class="container">
    <h2 class="text-center">{{ appName }}</h2>
    <button
      class="btn btn-success btn-block"
      @click="increment"
    >
      Incrementar
    </button>
    <div class="alert alert-secondary text-center mt-3">
      {{ counter }}
    </div>
    <button
      class="btn btn-danger btn-block"
      @click="decrement"
    >
      Decrementar
    </button>
  </div>
~~~