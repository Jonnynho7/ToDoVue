<script setup>
import { reactive } from 'vue'
import Cabecalho from './components/Cabecalho.vue'
import Formulario from './components/Formulario.vue'
import Todo from './components/Todo.vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemp: '',
  tarefas: [
    { titulo: 'Estudar ES6', finalizada: false },
    { titulo: 'Estudar Sass', finalizada: false },
  ]
})

const getTarefasPendentes = () => estado.tarefas.filter(tarefa => !tarefa.finalizada)
const getTarefasFinalizadas = () => estado.tarefas.filter(tarefa => tarefa.finalizada)

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case 'pendentes': return getTarefasPendentes()
    case 'finalizadas': return getTarefasFinalizadas()
    default: return estado.tarefas
  }
}

const cadastraTarefa = () => {
  if (estado.tarefaTemp.trim() === '') return
  estado.tarefas.push({ titulo: estado.tarefaTemp.trim(), finalizada: false })
  estado.tarefaTemp = ''
}
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario
      :troca-filtro="evento => estado.filtro = evento.target.value"
      :tarefa-temp="estado.tarefaTemp"
      :cadastra-tarefa="cadastraTarefa"
      :edita-temp="evento => estado.tarefaTemp = evento.target.value"
    />
    <Todo :tarefas="getTarefasFiltradas()" />
  </div>
</template>
