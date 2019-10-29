<template>
    <div>
        <li class="list-group-item" :class="todo.done? 'done' : ''">
            <input 
            type="checkbox" 
            @change="toggleDone(todo.id)" 
            :checked="todo.done">
            {{todo.name}}
            <span class="float-right" @click.prevent="deleteTodo(todo.id)"> [x] </span>    
        </li>
    </div>
</template>

<script>
export default {
    props:['todo'],
    methods:{
        deleteTodo(todoId){
            this.$emit('delete-todo', todoId)
        },
        toggleDone(todoId){
            this.$emit('complete-todo', todoId)
        }
    }
}
</script>

<style scoped>
span {
    color: red;
    cursor: pointer;
}
.done {
    text-decoration: line-through;
}
</style>