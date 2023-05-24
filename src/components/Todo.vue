<script setup>
const props = defineProps(['tarefas'])
</script>

<template>
    
  <ul class="list-group mt-4">
    <li v-for="tarefa in props.tarefas" class="list-group-item">
      <input @change="(e)=> tarefa.finalizada = e.target.checked " type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
      <label :class="{done: tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">
       {{ tarefa.titulo }}
      </label>
    </li>
  </ul>
</template>