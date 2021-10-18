<template>
    <div class="container grid-xs py-2">
      <img class="img-responsive img-tarefas" src="./assets/tarefas.png" alt="Tarefas">
      <form @submit.prevent="addTodo(todo)">
        <div class="input-group">
          <input type="text" v-model="todo.description" class="form-input" v-bind:class="{ preencherCampo: todo.empty }" placeholder="New todo">
          <button class="btn btn-primary input-goup-btn">Add</button>
        </div>
        <span v-if="todo.empty">Preencha o campo!</span>
      </form>
      <div class="todo-list">
        <todo v-for="t in todos" :key="t.id" @toggle='toggleTodo' @remove="removeTodo" :todo="t"/>
      </div>
    </div>

</template>

<script>
import Todo from './components/Todo'
export default {  
  components: {Todo},
  data() {
    return { todos: [], todo: { checked:false, empty:false}}
  }, 
  methods: {
    addTodo(todo) {
      if(todo.description){
        todo.id = Date.now()
        this.todos.push(todo)
        this.todo = {checked: false, empty: false} 
      } else {
        todo.empty = true
      }
    },
    toggleTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id);
      if(index > -1) {
        const checked = !this.todos[index].checked
        checked == checked
        this.$set(this.todos, index, {...this.todos[index], checked})
      }
    },
    removeTodo(todo) {
      const index = this.todos.findIndex(item => item.id === todo.id)
      if (index > -1){
        this.$delete(this.todos, index)
      }
    },
  }
}

</script>

<style scoped>
.img-tarefas {
  max-width: 200px;
  margin: 20px auto 60px;
  border-radius: 40px;
  }
.todo-list{
  padding-top: 2rem;
}
.tile-content {
  list-style: none;
}
.preencherCampo{
  border: 1px solid #ff0000;
}
</style>
