<script setup>
import { reactive } from "vue";
import cabecalho from "./components/cabecalho.vue";
import Form from "./components/Form.vue";
import ListaDeTarefas from "./components/ListaDeTarefas.vue";
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
    <cabecalho :tarefas-pendentes="tarefasPendentes().length" />
    <Form
      :trocar-filtro="(evento) => (estado.filtro = evento.target.value)"
      :tarefa-tempo="estado.tarefaTempo"
      :edita-tarefa="(evento) => (estado.tarefaTempo = evento.target.value)"
      :cadastra-tarefa="cadastraTarefa"
    ></Form>
    <ListaDeTarefas :tarefas="tarefasFiltradas()"></ListaDeTarefas>
  </div>
</template>
