<template>
    <form action="#" @submit.prevent="addTodo">
        <div class="form-group">
        <label for="Todo">Todo :</label>
        <input autofocus type="text" class="form-control" v-model="todo" placeholder="Create new Todo">
        </div>
        <div class="form-group">
        <button class="btn btn-primary">Add</button>
        </div>
    </form>
</template>

<script>
export default {
    data(){
        return{
            todo:null
        }
    },
    methods:{
        addTodo(){
            if(this.todo !== null){
                this.$emit('add-todo', this.todo)
                this.todo = null
            }
        }
    }
}
</script>