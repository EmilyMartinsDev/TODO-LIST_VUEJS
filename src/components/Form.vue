<script setup>
const props = defineProps(["cadastraTarefa", "tarefaTmp", "trocarFiltro", "EditaTarefaTmp"])
</script>

<template>
    <form action="" @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTmp" @change="props.EditaTarefaTmp" type="text"
                    placeholder="digite aqui a descrição da tarefa" class="form-control" required>
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary" type="submit">cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change=" props.trocarFiltro" class="form-control">
                    <option value="todas">Todas Tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>