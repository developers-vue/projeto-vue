<script>
export default {
  // props: dados que o componente RECEBE de App.vue
  props: {
    tarefas: {
      type: Array,
      required: true
    }
  },

  // emits: eventos que o componente ENVIA para App.vue
  emits: ['alternar', 'excluir']
}
</script>

<template>
  <p v-if="tarefas.length === 0" class="vazio">
    Nenhuma tarefa por aqui. Adicione sua primeira tarefa!
  </p>

  <ul v-else class="lista">
    <li
      v-for="tarefa in tarefas"
      :key="tarefa.id"
      class="item"
      :class="{ concluida: tarefa.concluida }"
    >
      <div class="info">
        <span class="nome">{{ tarefa.nome }}</span>
        <span
          class="status"
          :class="tarefa.concluida ? 'status-ok' : 'status-pendente'"
        >
          {{ tarefa.concluida ? 'Concluída' : 'Pendente' }}
        </span>
      </div>

      <div class="acoes">
        <button class="btn-concluir" @click="$emit('alternar', tarefa.id)">
          {{ tarefa.concluida ? 'Desfazer' : 'Concluir' }}
        </button>
        <button class="btn-excluir" @click="$emit('excluir', tarefa.id)">
          Excluir
        </button>
      </div>
    </li>
  </ul>
</template>

<style scoped>
.lista {
  list-style: none;
  margin: 0;
  padding: 0;
}

.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
  margin-bottom: 10px;
  padding: 14px;
  border: 1px solid #e5e7f2;
  border-left: 5px solid #f59e0b;
  border-radius: 10px;
  background-color: #fafbff;
}

.item.concluida {
  border-left-color: #16a34a;
}

.item.concluida .nome {
  text-decoration: line-through;
  color: #8a90a8;
}

.info {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.nome {
  font-size: 16px;
  font-weight: bold;
}

.status {
  align-self: flex-start;
  padding: 3px 10px;
  border-radius: 20px;
  font-size: 12px;
  font-weight: bold;
}

.status-pendente {
  background-color: #fef3c7;
  color: #92400e;
}

.status-ok {
  background-color: #dcfce7;
  color: #166534;
}

.acoes {
  display: flex;
  gap: 8px;
}

button {
  padding: 8px 14px;
  border: none;
  border-radius: 7px;
  color: #ffffff;
  font-size: 14px;
  cursor: pointer;
}

.btn-concluir {
  background-color: #16a34a;
}

.btn-concluir:hover {
  background-color: #15803d;
}

.btn-excluir {
  background-color: #dc2626;
}

.btn-excluir:hover {
  background-color: #b91c1c;
}

.vazio {
  margin: 0;
  padding: 30px 10px;
  text-align: center;
  color: #6b7190;
}

@media (max-width: 500px) {
  .item {
    flex-direction: column;
    align-items: flex-start;
  }
}
</style>