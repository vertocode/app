<template>
  <div>
    <label>{{ customLabel }}</label>
    <input
        type="range"
        :value="valor"
        :class="inputClasses"
        @change="atualizar"
        :min="min"
        :max="max"
        :step="step">
  </div>
</template>

<script>
  export default {
    inheritAttrs: false,
    model: {
      prop: 'valor',
      event: 'change'
    },
    props: {
      label: String,
      valor: [Number, String],
      min: [Number, String],
      max: [Number, String],
      step: [Number, String],
      inputClasses: [String, Object, Array]
    },
    data() {
      return {
        valorAtual: this.valor || this.$attrs.min
      }
    },
    computed: {
      customLabel() {
        return `${this.label} (R$ ${this.valorAtual})`
      }
    },
    methods: {
      atualizar(event) {
        const valor = event.target.value
        this.$emit('change', valor)
        this.valorAtual = valor
      }
    }
  }
</script>