<template>
    <div v-if="contato">
        <h3 class="font-weight-light">Nome: {{ contato.nome }}</h3>

        <form @submit.prevent="salvar">
            <div class="form-group">
                <label>Nome</label>
                <input 
                    type="text" 
                    class="form-control" 
                    placeholder="Insira o nome" 
                    v-model="contato.nome">
            </div>
            <div class="form-group">
                <label>Email</label>
                <input 
                    type="email" 
                    class="form-control" 
                    placeholder="Insira o email"
                    v-model="contato.email">
            </div>

            <button 
                type="button" 
                class="btn btn-secondary mt-4 mb-4 mr-2" 
                @click="$router.back()">
                    Voltar
            </button>
            <button 
                type="submit" 
                class="btn btn-success">
                    Salvar
            </button>
        </form>

    </div>
</template>

<script>

import EventBus from './../../event-bus'

export default {
    props: ['id'],
    data() {
        return {
            contato: undefined,
            estaCancelando: true
        }
    },
    beforeRouteEnter(to, from, next) {
        next(vm => {
            vm.contato = EventBus.buscarContato(+to.params.id)
        })
    },
    beforeRouteLeave(to, from, next) {
        console.log('beforeRouteLeave')
        this.estaCancelando
            ? next(window.confirm('Deseja realmente sair?'))
            : next()
    },
    methods: {
        salvar() {
            EventBus.editarContato(this.contato)
            this.estaCancelando = false
            this.$router.push('/contatos')
        }
    }
}
</script>

