<script setup>
import { reactive } from 'vue';
import Header from './components/Header.vue';
import Form from './components/Form.vue';
import Todo from './components/Todo.vue';

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
    <Header :tarefas-pendentes="MostartarefasPendentes().length"/>
    <Form :trocar-filtro="e=> estado.filtro = e.target.value" :tarefa-tmp="estado.tarefaTmp" :edita-tarefa-tmp="(e)=>estado.tarefaTmp = e.target.value" :cadastra-tarefa="cadastraTarefa"/>
    <Todo :tarefas="getTarefasFiltradas()"/>
</div>
</template>

<style scoped>
.done{
  text-decoration: line-through;
}
</style>
