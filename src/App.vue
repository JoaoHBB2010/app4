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
const aviso = ref(false);
const alteracao = ref(-1);

function add(){
    
    if(novaTarefa.value.length < 5){
        aviso.value = true;
    }
    else{
        if(alteracao.value == -1){
        tarefas.value.push(novaTarefa.value);
        novaTarefa.value = '';
        }
        else{
            tarefas.value.splice(alteracao.value, 1, novaTarefa.value);
            novaTarefa.value = '';
            alteracao.value = -1;
        }
    }
}
function deleteTarefa(item){
    const posicao = tarefas.value.indexOf(item);
    tarefas.value.splice(posicao,1);
}
function editarTarefa(item){
    alteracao.value = tarefas.value.indexOf(item);
    novaTarefa.value = item;
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
                <span>
                    <a href="#" @click.prevent="editarTarefa(tarefa)">Edit</a>
                    <a href="#" @click.prevent="deleteTarefa(tarefa)">Delet</a>
                </span>
            </li>
        </ul>
        <button @click="tarefas.sort()">Ordenar</button>
    </div>
   
</template>

<style scoped>
.aviso{
    color: white;
    background: red;
}
</style>
