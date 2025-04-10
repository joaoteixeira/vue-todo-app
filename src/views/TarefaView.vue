<template>
    <div>
        <h1 class="text-3xl">Lista de tarefas</h1>

        <button v-if="!abrirForm" @click="abrirForm = true">Nova tarefa</button>

        <div v-if="abrirForm">
            <form>
                <input type="text" v-model="descricao" placeholder="Informe 
                a descrição da tarefa"/>
                <button @click="adicionar">Adicionar</button>
            </form>
        </div>

        <table class="table">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Id</th>
                    <th>Descrição</th>
                    <th>Feito?</th>
                    <th>Ação</th>
                </tr>
            </thead>
            
            <tbody>
                <tr v-for="(item, index) in tarefas" :key="index">
                    <td>{{ index }}</td>
                    <td>{{ item.id }}</td>
                    <td>{{ item.descricao }}</td>
                    <td>{{ item.feito ? 'Sim' : 'Não' }}</td>
                    <td>
                        <button v-if="!item.feito" @click="finalizar(item.id)">Finalizar</button>
                        <button @click="remover(item.id)">X</button>
                    </td>
                </tr>
            </tbody>
            
        </table>

    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
    props: {},
    data() {
        return {
            tarefas: [
                {
                    id: 1,
                    descricao: 'Estudar Javascript',
                    feito: false
                },
                {
                    id: 2,
                    descricao: 'Estudar Typescript',
                    feito: false
                },
            ],
            descricao: null,
            abrirForm: false,
        }
    },

    methods: {
        remover(id: number) {
            const novaLista = this.tarefas.filter(item => {
                return item.id != id;
            });

            this.tarefas = novaLista;
        },

        adicionar() {
            if(this.descricao != null) {
                const id: number = this.tarefas.length + 1;

                const novaTarefa = {
                    id: id,
                    descricao: this.descricao,
                    feito: false
                }

                this.tarefas.push(novaTarefa);
                this.descricao = null;
                this.abrirForm = false;
            }
        },

        finalizar(id: Number) {

            for(const item of this.tarefas) {
                if(item.id == id) {
                    item.feito = true;
                }
            }

        }
    }
})

</script>