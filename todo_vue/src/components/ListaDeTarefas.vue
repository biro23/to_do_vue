<template>
  <ul class="list-group mt-4">
    <li
      class="list-group-item"
      v-for="tarefa in tarefasFiltradas"
      :key="tarefa.id"
    >
      <input
        @change="(evento) => (tarefa.finalizada = evento.target.checked)"
        :checked="tarefa.finalizada"
        :id="tarefa.id"
        type="checkbox"
      />
      <label :class="{ done: tarefa.finalizada }" class="ms-3" :for="tarefa.id">
        {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>

<script setup>
import { ref } from "vue";

const tarefasFiltradas = ref([]);

onMounted(() => {
  tarefasFiltradas.value = getTarefasFiltradas();
});
</script>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
