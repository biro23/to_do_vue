<script setup>
import { reactive } from "vue";

// criando um estado para as tarefas, tarefaTemp: '', vai começar com uma string vazia
const estado = reactive({
  filtro: "todas",
  tarefaTemp: " ",
  tarefas: [
    { titulo: "Estudar ES6", finalizada: false },
    {
      // outra tarefa
      titulo: "Estudar Sass",
      finalizada: false,
    },
    {
      titulo: "Ir para a academia",
      finalizada: true,
    },
  ],
});

// aqui vamos filtrar o estado.tarefas
const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  switch (estado.filtro) {
    case "Finalizadas":
      return getTarefasFinalizadas();
    case "Pendentes":
      return getTarefasPendentes();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemp,
    finalizada: false,
  };
  estado.tarefas.push(tarefaNova);
  estado.tarefaTemp = '';
};
</script>

<template>
  <!-- aqui vamos ter um container, mais um cabecalho, aplicar o boostrap nesta parte -->
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <!-- aqui teremos um formulario, uma linha, com o required, o navegador da a mensagem de enviar cadastro -->
    <form @submit.prevent="cadastraTarefa">
      <div class="row">
        <div class="col">
          <input
            :value="estado.tarefaTemp"
            @change="(evento) => (estado.tarefaTemp = evento.target.value)"
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
          <select
            @change="(evento) => (estado.filtro = evento.target.value)"
            class="form-control"
          >
            <option value="todas">Todas tarefas</option>
            <option value="Finalizadas">Finalizadas</option>
            <option value="Pendentes">Pendentes</option>
          </select>
        </div>
      </div>
    </form>
    <!-- lista nao ordenada  -->
    <ul class="list-group mt-4">
      <li
        class="list-group-item"
        v-for="tarefa in getTarefasFiltradas()"
        :key="tarefa.titulo"
      >
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
        >
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
