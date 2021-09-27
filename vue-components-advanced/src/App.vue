<template>
  <div id="app" class="container">

    <h1>Componentes Dinâmicos</h1>

    <button @click="componentSelecionado = 'Home'">Home</button>
    <button @click="componentSelecionado = 'PostLista'">PostLista</button>
    <button @click="componentSelecionado = 'Sobre'">Sobre</button>
    <button @click="componentSelecionado = 'Assincrono'">Assincrono</button>

    <keep-alive :exclude="['Home', 'PostLista']">
      <component
          :is="componentSelecionado"
          v-bind="propsAtuais">
      </component>
    </keep-alive>

  </div>
</template>

<script>

import PostLista from './components/PostLista.vue'
import Home from './components/Home.vue'
import Sobre from './components/Sobre.vue'

export default {
  components: {
    Assincrono: () => ({
      component: import('./components/Assincrono.vue'),
      loading: { template: `<p>Carregando...</p>` },
      error: { template: `<p>Erro ao carregar component!</p>` },
      delay: 200,
      timeout: 3000
    }),
    PostLista,
    Home,
    Sobre
  },
  data() {
    return {
      componentSelecionado: 'Home',
      posts: [
        {id: 1, titulo: 'Components no Vue', conteudo: 'Components são umas das peças mais importantes', autor: 'Everton Vanoni'},
        {id: 2, titulo: 'Distribuindo conteudos com slots', conteudo: 'Slots podem ser usados como repositorios de codigo HTML', autor: 'Everton Vanoni'}
      ]
    }
  },
  computed: {
    propsAtuais() {
      return this.componentSelecionado === 'PostLista'
      ? { posts: this.posts }
          : {}
    }
  }
}
</script>

<style scoped>

  .container {
    width: 960px;
    margin: auto;
  }

</style>