<template>
  <li>
    <span>{{ contato.nome }}</span>
    <!--
    <router-link
        :to="{ path: `/contatos${contato.id}` }"
        class="btn btb-info btn-sm float-right">
      Detalhes
    </router-link>
    -->

    <button
        class="btn btb-info btn-sm float-right m-2"
        @click="verDetalhes">
      Detalhes
    </button>
  </li>
</template>

<script>
  export default {
    props: {
      contato: {
        type: Object,
        required: true
      }
    },
    methods: {
      verDetalhes() {
        this.$router.push(`/contatos/${this.contato.id}`)
      }
    }
  }
</script>