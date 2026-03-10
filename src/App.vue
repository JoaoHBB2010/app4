<script setup>
import { ref } from 'vue'
const tarefas = ref([
    'Prova Matemática',
    'Prova Geografia',
    'Trabalho Sociologia',
    'Seminário Português',
    'Seminário de Educação Física',
    'Seminário Geografia',
    'Prova Física'
]);
const novaTarefa = ref('');
const aviso = ref(false)
function add(){
    
    if(novaTarefa.value.length < 5){
        aviso.value = true;
    }
    else{
        tarefas.value.push(novaTarefa.value);
        novaTarefa.value = '';
    }
}
function deleteTarefa(item){
    const posicao = tarefas.value.indexOf(item);
    tarefas.value.splice(posicao,1);
}

</script>

<template>
    <div class="container">
        <h1>Lista de Tarefas</h1>
        <input type="text" v-model="novaTarefa" @keyup.enter = "add" @input="aviso = false">
        <button @click="add" >Add</button> 
     <div v-show="aviso" class="aviso">Insira ao menos 5 caracteres </div>
        <ul>
            <li v-for="tarefa in tarefas" :key="tarefa">
                {{ tarefa }}
                <span><a href="#" @click.prevent="deleteTarefa(tarefa)">Excluir</a></span>
            </li>
        </ul>
    </div>
   
</template>

<style scoped>
.aviso{
    color: white;
    background: red;
}
</style>
