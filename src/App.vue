<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTmp: '',
  tarefas: [
  { titulo: 'estudar Es6',
    finalizada: false,
  },
  { titulo: 'estudar SASS',
    finalizada: true,
  },
  { titulo: 'Academia',
    finalizada: true,
  }
  ]
})

function MostartarefasPendentes(){
   
  return estado.tarefas.filter(tarefa=>!tarefa.finalizada);
}

function MostartarefasFinalizadas(){
   
   return estado.tarefas.filter(tarefa=>tarefa.finalizada);
 }
 

const getTarefasFiltradas = ()=>{
  const {filtro} = estado;

  switch(filtro){
    case 'pendentes':
      return MostartarefasPendentes();
    case 'finalizadas':
      return MostartarefasFinalizadas();
      default:
        return estado.tarefas;
  }

}
const cadastraTarefa = (e)=>{
  const novaTarefa = {
    titulo: estado.tarefaTmp,
    finalizada: false
  }
  estado.tarefas.push(novaTarefa);
  estado.tarefaTmp = '';
}
</script>

<template>
  <div class="container">
    <header class="p-5 mt-4 mb-4 bg-light rounded-5">
      <h1>Minhas tarefas</h1>
      <p>Você possui {{ MostartarefasPendentes().length }} tarefas pendentes</p>
    </header>

  <form action="" @submit.prevent="cadastraTarefa">
    <div class="row">
      <div class="col">
        <input :value="estado.tarefaTmp" @change="(e)=> estado.tarefaTmp = e.target.value" type="text" placeholder="digite aqui a descrição da tarefa" class="form-control" required>
      </div>
      <div class="col-md-2">
          <button class="btn btn-primary" type="submit">cadastrar</button>
      </div>
      <div class="col-md-2">
        <select @change="(e)=> estado.filtro = e.target.value" class="form-control">
          <option value="todas">Todas Tarefas</option>
          <option value="pendentes">Pendentes</option>
          <option value="finalizadas">Finalizadas</option>
        </select>
      </div>
    </div>
  </form>
  <ul class="list-group mt-4">
    <li v-for="tarefa in getTarefasFiltradas()" class="list-group-item">
      <input @change="(e)=> tarefa.finalizada = e.target.checked " type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo">
      <label :class="{done: tarefa.finalizada}" :for="tarefa.titulo" class="ms-3">
       {{ tarefa.titulo }}
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
