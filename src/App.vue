<script>
import FormTarefa from './components/FormTarefa.vue'
import ListaTarefas from './components/ListaTarefas.vue'

export default {
  components: { FormTarefa, ListaTarefas },

  data() {
    return {
      tarefas: [],
      proximoId: 1,
    }
  },

  computed: {
    total() {
      return this.tarefas.length
    },
    concluidas() {
      return this.tarefas.filter(tarefa => tarefa.concluida).length
    },
    pendentes() {
      return this.tarefas.filter(tarefa => !tarefa.concluida).length
    },

  },

  methods: {
    adicionarTarefa(nome) {
      this.tarefas.push({
        id: this.proximoId,
        nome: nome,
        concluida: false
      })
      this.proximoId++
    },

    alternarTarefa(id) {
      const tarefa = this.tarefas.find(item => item.id === id)
      tarefa.concluida = !tarefa.concluida
    },

    excluirTarefa(id) {
      this.tarefas = this.tarefas.filter(item => item.id !== id)
    }
  }
}
</script>

<template>
  <div class="container">
    <header class="cabecalho">
      <h1>Fast<span>Tasks</span></h1>
      <p class="slogan">Organize suas tarefas. Simplifique seu dia.</p>
      <p class="descricao">
        Cadastre, acompanhe e conclua suas tarefas em um só lugar.
      </p>
    </header>

    <section class="card">
      <h2>Nova tarefa</h2>
      <FormTarefa @adicionar="adicionarTarefa" />
    </section>

    <section class="indicadores">
      <div class="indicador">
        <strong>{{ total }}</strong>
        <span>Total</span>
      </div>
      <div class="indicador pendentes">
        <strong>{{ pendentes }}</strong>
        <span>Pendentes</span>
      </div>
      <div class="indicador concluidas">
        <strong>{{ concluidas }}</strong>
        <span>Concluídas</span>
      </div>
    </section>

    <section class="card">
      <h2>Minhas tarefas</h2>

      <ListaTarefas
        :tarefas="tarefas"
        @alternar="alternarTarefa"
        @excluir="excluirTarefa"
      />
    </section>
    
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 30px 16px;
  font-family: Arial, sans-serif;
  background-color: #f4f6fb;
  color: #263238;
}

.container {
  max-width: 720px;
  margin: 0 auto;
}

.cabecalho {
  margin-bottom: 24px;
  text-align: center;
}

.cabecalho h1 {
  margin: 0;
  font-size: 40px;
  color: #263238;
}

.cabecalho h1 span {
  color: #4f46e5;
}

.slogan {
  margin: 6px 0;
  font-weight: bold;
  color: #4f46e5;
}

.descricao {
  margin: 0;
  color: #6b7190;
}

.card {
  margin-bottom: 20px;
  padding: 24px;
  border-radius: 14px;
  background-color: #ffffff;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.06);
}

.card h2 {
  margin: 0 0 16px;
  font-size: 20px;
}

.indicadores {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 14px;
  margin-bottom: 20px;
}

.indicador {
  padding: 18px;
  border-radius: 14px;
  background-color: #ffffff;
  box-shadow: 0 6px 20px rgba(0, 0, 0, 0.06);
  text-align: center;
}

.indicador strong {
  display: block;
  font-size: 30px;
  color: #4f46e5;
}

.indicador.pendentes strong {
  color: #d97706;
}

.indicador.concluidas strong {
  color: #16a34a;
}

.indicador span {
  font-size: 14px;
  color: #6b7190;
}
</style>