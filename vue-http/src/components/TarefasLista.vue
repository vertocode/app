<template>
    <div>

        <div class="row">
          <div class="col-sm-10">
            <h1 class="font-weight-light">Lista de Tarefas</h1>
          </div>
          <div class="col-sm-2">
            <button
              class="btn btn-primary float-right"
              @click="exibirFormularioCriarTarefa"
              v-if="!exibirFormulario">
                <i class="fa fa-plus mr-2"></i>
                <span>Criar</span>
            </button>
          </div>
        </div>

        <ul class="list-group" v-if="tarefas.length > 0">
            <TarefasListaIten
                v-for="tarefa in tarefasOrdenadas"
                :key="tarefa.id"
                :tarefa="tarefa"
                @editar="selecionarTarefa"
                @concluir="editarTarefa"
                @deletar="deletarTarefa" />
        </ul>

        <p v-else>Nenhuma tarefa criada.</p>

        <TarefaSalvar
          v-if="exibirFormulario"
          :tarefa="tarefaSelecionada"
          @criar="criarTarefa"
          @editar="editarTarefa"
        />

    </div>
</template>

<script>

import axios from 'axios'
import config from './../config/config'

import TarefaSalvar from './TarefaSalvar.vue'
import TarefasListaIten from './TarefasListaIten.vue'

export default {
    components: {
        TarefaSalvar,
        TarefasListaIten
    },
    data() {
        return {
            tarefas: [],
            exibirFormulario: false,
            tarefaSelecionada: undefined
        }
    },
    computed: {
      tarefasOrdenadas() {
        return this.tarefas.slice().sort((t1,t2) => {
          if (t1.concluido === t2.concluido) {
            return t1.titulo < t2.titulo
              ? -1
              : t1.titulo > t2.titulo
                ? 1
                : 0
          }
          return t1.concluido - t2.concluido
        })
      }
    },
    created() {
      axios.get(`${config.apiURL}/tarefas`)
       .then((response) => {
         this.tarefas = response.data
         console.log(`API inject with sucess: ${response.data}`)
       })
    },
    methods: {
      criarTarefa(tarefa) {
        console.log('Executou por fora')
        axios.post(`${config.apiURL}/tarefas`, tarefa)
        .then((response) => {
          this.tarefas.push(response.data)
          this.exibirFormulario = false
          console.log('Executou por dentro')
          this.resetar()
        })
      },
      selecionarTarefa(tarefa) {
        this.tarefaSelecionada = tarefa
        this.exibirFormulario = true
      },
      editarTarefa(tarefa) {
        console.log('Editar', tarefa)
        axios.put(`${config.apiURL}/tarefas/${tarefa.id}`, tarefa)
        .then(response => {
          console.log(`PUT /tarefas/${tarefa.id}`, response)
          const indice = this.tarefas.findIndex(t => t.id === tarefa.id)
          this.tarefas.splice(indice, 1, tarefa)
          this.resetar()
        })
      },
      resetar() {
        this.tarefaSelecionada = undefined
        this.exibirFormulario = false
      },
      deletarTarefa(tarefa) {
        const confirmar = confirm(`Deseja deletar a tarefa "${tarefa.titulo}"`)
        if (confirmar) {
          axios.delete(`${config.apiURL}/tarefas/${tarefa.id}`)
            .then(() => {
              const indice = this.tarefas.findIndex(t => t.id === tarefa.id)
              this.tarefas.splice(indice, 1)
            })
        }
      },
      exibirFormularioCriarTarefa() {
        if(this.tarefaSelecionada) {
          this.tarefaSelecionada = undefined
          return
        }
        this.exibirFormulario = !this.exibirFormulario
      }
    }
}
</script>
