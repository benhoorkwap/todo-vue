<script>

    export default {
       
        data(){
            return {
                todoText: "",
                todos: []
            }
        },

        computed: {
            canShowListItems() {
                return this.todos.length > 0
            }
        },

        methods: {
            addTodo(){
                if(this.todoText.length === 0) return
                if(this.todos.findIndex((todo) => todo.text === this.todoText) !== -1) return
                this.todos.push({text: this.todoText, id: this.todos.length + 1})
                this.todoText = ""
            },

            removeTodo(id) {
                let index = this.todos.findIndex(todo => todo.id === id)
                this.todos.splice(index, 1)
            }
        }
    }
</script>


<template>
    <div class="todos">
        <input class="todosInput" v-model="todoText" @keydown.enter="addTodo">
        <button class="addTodo" @click="addTodo">Add Todo</button>
        <ul class="todoList" v-show="canShowListItems">
            <li class="todoListItem" v-for="todo in todos" :key="todo.id">
                <span class="todoText">{{todo.text}}</span>
                <button @click="removeTodo(todo.id)" class="exitBtn">x</button>
            </li>
        </ul>

    </div>
</template>


<style scoped>
    .todos {
        display: grid;
        grid-template-columns: 25rem 5rem;
        gap: 0.675rem;
    }

    .todosInput {
        height: 2.5rem;
    }

    .addTodo {
        background-color: #007fff;
        border: none;
        border-radius: 0.3375rem;
        color: #fff;
    }

    .todoList {
        grid-column: 1 / span 2;
        margin: 0;
        padding: 0;
    
    }

    .todoListItem {
        list-style: none;
        width: 100%;
        border-left: 0.5rem solid lightblue;
        height: 2.5rem;
        background-color: rgba(169, 169, 169, 0.2);
        align-items: center;

        display: flex;
        padding-right: 0.3375rem;
    
    }

    .todoText {
        text-align: left;
        flex: 1;
    }

    .exitBtn {
        background-color: transparent;
        width:2rem;
        border: none
    }
</style>
