<script setup>
import { reactive } from 'vue';

const estado = reactive({
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

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light roundend-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui 7 tarefas pendentes
      </p>
    </header>
    <form>
      <div class="row">
        <div class="col">
          <input type="text" placeholder="Digite sua tarefa" class="form-control">
        </div>
        <div class="col md-1">
          <button type="submit" class="btn btn-primary">Adicionar tarefa</button>
        </div>
        <div class="col md-2">
          <select class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="todas">Tarefas pendentes</option>
            <option value="todas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefas in estado.tarefas">
        <input :checked="tarefas.finalizada" :id="tarefas.titulo" type="checkbox">
        <label class="ms-3" :for="tarefas.titulo">
          {{ tarefas.titulo }}
        </label>
      </li>
    </ul>
  </div>

</template>

<style scoped></style>
