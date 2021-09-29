<template>
    <ContatosLista :busca="busca" />
</template>

<script>

import ContatosLista from './../../components/contatos/ContatosLista.vue'

export default {
    components: {
        ContatosLista
    },
    props: ['busca']
}
</script>