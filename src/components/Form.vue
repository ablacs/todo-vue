<script setup>
const props = defineProps([
  "cadastraTarefa",
  "tarefaTempo",
  "trocarFiltro",
  "editaTarefa",
]);
</script>
<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          :value="props.tarefaTempo"
          @change="props.editaTarefa"
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
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="Pendentes">Pendentes</option>
          <option value="finalizadas">finalizadas</option>
        </select>
      </div>
    </div>
  </form>
</template>
