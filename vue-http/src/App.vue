<template>
  <div id="app">

    <div class="jumbotron jumbotron-fluid">
      <div class="container">
        <h1 class="display-4">Requisições HTTP no Vue</h1>
        <p class="lead">Usando a biblioteca Axios para fazer chamadas Ajax à uma API REST</p>
      </div>
    </div>

    <div class="container">
      <TarefasLista />
    </div>

  </div>
</template>

<script>

import TarefasLista from './components/TarefasLista'

export default {
  components: {
    TarefasLista
  }
}
</script>