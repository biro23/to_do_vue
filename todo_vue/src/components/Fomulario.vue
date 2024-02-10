<template>
  <form @submit.prevent="props.cadastraTarefa">
    <div class="row">
      <div class="col">
        <input
          v-model="props.tarefaTemp"
          required
          type="text"
          placeholder="Digite aqui a descrição da tarefa"
          class="form-control"
        />
      </div>
      <div class="col-md-2">
        <button type="submit" class="btn btn-primary">Cadastrar</button>
      </div>

      <!-- aqui vai outra coluna -->
      <div class="col-md-2">
        <select @change="props.trocarFiltro" class="form-control">
          <option value="todas">Todas tarefas</option>
          <option value="finalizadas">Finalizadas</option>
          <option value="pendentes">Pendentes</option>
        </select>
      </div>
    </div>
  </form>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps(["cadastraTarefa", "tarefaTemp", "trocarFiltro"]);
</script>
