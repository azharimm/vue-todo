<template>
  <div id="app" class="container">
    <div class="row mt-2">
      <div class="col-md-6 offset-3">
        <div class="card">
          <div class="card-header">
            Todo App
          </div>
          <div class="card-body">
            <add-todo @add-todo="addTodo"></add-todo>
            <hr>
            <ul class="list-group">
              <todos 
              :todo="todo" 
              v-for="todo in todos" 
              :key="todo.id" 
              @delete-todo="deleteTodo"
              @complete-todo="completeTodo">
              </todos>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import AddTodo from './components/AddTodo'
import Todos from './components/Todos'
export default {
  name: 'app',
  data(){
    return{
      todos:[]
    }
  },
  components:{
    AddTodo,
    Todos
  },
  mounted(){
      if(localStorage.getItem('todos')){
        this.todos = JSON.parse(localStorage.getItem('todos'))
      }
  },
  methods:{
    saveStorage(todos){
      localStorage.setItem('todos', JSON.stringify(todos))
    },
    addTodo(value){
      this.todos.unshift(
        {id: Date.now().toString() , name:value, done: false}
      )
      this.saveStorage(this.todos)
      this.todo = null
    },
    deleteTodo(todoId){
      this.todos = this.todos.filter((todo) => {
        return todo.id !== todoId
      })
      this.saveStorage(this.todos)
    },
    completeTodo(todoId){
      const index = this.todos.findIndex(todo => {
        return todo.id === todoId
      })
      this.todos[index].done = !this.todos[index].done;
      this.saveStorage(this.todos)
    }
  }
}
</script>

<style>

</style>
