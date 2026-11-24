<script>
export default {
  // emits: avisa quais eventos este componente envia para App.vue
  emits: ['adicionar'],

  data() {
    return {
      nome: '',
      erro: ''
    }
  },

  methods: {
    enviar() {
      const texto = this.nome.trim()

      if (texto === '') {
        this.erro = 'Digite o nome da tarefa.'
        return
      }

      this.erro = ''
      this.$emit('adicionar', texto) // envia o texto para o App.vue
      this.nome = ''                 // limpa o campo
    }
  }
}
</script>

<template>
  <form class="form" @submit.prevent="enviar">
    <div class="linha">
      <input
        type="text"
        v-model="nome"
        placeholder="Ex.: Organizar apresentação Vue.js"
      />
      <button type="submit">Adicionar</button>
    </div>

    <p v-if="erro" class="erro">{{ erro }}</p>
  </form>
</template>

<style scoped>
.linha {
  display: flex;
  gap: 10px;
}

input {
  flex: 1;
  padding: 12px;
  border: 1px solid #d5d9eb;
  border-radius: 8px;
  font-size: 16px;
}

input:focus {
  outline: none;
  border-color: #4f46e5;
}

button {
  padding: 12px 20px;
  border: none;
  border-radius: 8px;
  background-color: #4f46e5;
  color: #ffffff;
  font-size: 15px;
  cursor: pointer;
}

button:hover {
  background-color: #4338ca;
}

.erro {
  margin: 10px 0 0;
  padding: 10px;
  border-radius: 8px;
  background-color: #fee2e2;
  color: #b91c1c;
  font-size: 14px;
}

@media (max-width: 500px) {
  .linha {
    flex-direction: column;
  }
}
</style>