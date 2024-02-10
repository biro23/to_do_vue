<script setup>
import { reactive } from "vue";
import Cabecalho from "./components/Cabecalho.vue";
import Formulario from "./components/Formulario.vue"; // Corrigido o import do componente Formulario
import ListaDeTarefas from "./components/ListaDeTarefas.vue"

// criando um estado para as tarefas, tarefaTemp: '', vai começar com uma string vazia
const estado = reactive({
  filtro: "todas",
  tarefaTemp: "",
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
  estado.tarefaTemp = "";
};
</script>

<template>
  <!-- aqui vamos ter um container, mais um cabecalho, aplicar o boostrap nesta parte -->
  <div class="container">
    <Cabecalho :tarefasPendentes="getTarefasPendentes.length"/> <!-- Corrigido a propriedade length -->
    <Formulario 
      v-bind:tarefaTemp="tarefaTemp" <!-- Corrigido aqui -->
      @input="(evento) => estado.tarefaTemp = evento.target.value"
      @submit="cadastraTarefa"
    />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
