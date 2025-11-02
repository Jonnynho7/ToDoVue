<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'Todas',
  tarefaTemp: '',
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,
    },
    {
      titulo: 'estudar Sass',
      finalizada: false
    },
    {
      titulo: 'fumar um Idris Elba',
      finalizada: true
    }
  ]
})


const getTarefasPendentes = () =>{
  return estado.tarefas.filter(tarefas => !tarefas.finalizada)
}

const getTarefasFinalizadas = () =>{
  return estado.tarefas.filter(tarefas => tarefas.finalizada)
}

const getTarefasFiltradas = () => {
  const {filtro} = estado;

  switch(filtro){
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
      default:
        return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const novaTarefa = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = '';
}

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light roundend-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemp" @change="evento => estado.tarefaTemp = evento.target.value" required type="text" placeholder="Digite sua tarefa" class="form-control">
        </div>
        <div class="col md-1">
          <button type="submit" class="btn btn-primary">Adicionar tarefa</button>
        </div>
        <div class="col md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefas in getTarefasFiltradas()">
        <input @change="evento => tarefas.finalizada = evento.target.checked" v-model="tarefas.finalizada" :id="tarefas.titulo" type="checkbox">
        <label :class="{done: tarefas.finalizada}" class="ms-3" :for="tarefas.titulo">
          {{ tarefas.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
