<script setup>
import { reactive } from "vue";
const estado = reactive({
  filtro: "todas",
  tarefaTempo: "",
  tarefa: [
    {
      titulo: "Estudar ES6",
      finalizada: false,
    },
    {
      titulo: "Estudar SASS",
      finalizada: false,
    },
    {
      titulo: "ir para a academia",
      finalizada: true,
    },
  ],
});
const tarefasPendentes = () => {
  return estado.tarefa.filter((tarefa) => !tarefa.finalizada);
};
const tarefasFinalizadas = () => {
  return estado.tarefa.filter((tarefa) => tarefa.finalizada);
};
const tarefasFiltradas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case "Pendentes":
      return tarefasPendentes();
    case "finalizadas":
      return tarefasFinalizadas();
    default:
      return estado.tarefa;
  }
};
const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTempo,
    finalizada: false,
  };
  estado.tarefa.push(tarefaNova);
  estado.tarefaTempo = "";
};
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ tarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input
            :value="estado.tarefaTempo"
            @change="(evento) => (estado.tarefaTempo = evento.target.value)"
            required
            type="text"
            placeholder="Digite a descrição da tarefa"
            class="form-control"
          />
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select
            @change="(evento) => (estado.filtro = evento.target.value)"
            class="form-control"
          >
            <option value="todas">Todas tarefas</option>
            <option value="Pendentes">Pendentes</option>
            <option value="finalizadas">finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in tarefasFiltradas()">
        <input
          @change="(evento) => (tarefa.finalizada = evento.target.checked)"
          :checked="tarefa.finalizada"
          :id="tarefa.titulo"
          type="checkbox"
        />
        <label
          :class="{ done: tarefa.finalizada }"
          class="ms-3"
          :for="tarefa.titulo"
          >{{ tarefa.titulo }}</label
        >
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
