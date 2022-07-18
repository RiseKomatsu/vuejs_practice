<template>
  <div class="container">
    <h2 class="">Todo app</h2>
    <div class="card">
      <div class="card-body col-12">
        <div class="d-flex justify-content-between">
          <h3>Enter todo</h3>
          <button type="button" class="btn btn-primary" style="submit" @click="deleteAll">delete all</button>
        </div>
        <div class="py-2">Name:<input v-model="todo.name"></div>
        <div class="py-2">Description:<input v-model="todo.description"></div>
        <div class="py-2">Deadline:<input v-model="todo.deadline"></div>
      <button type="button" class="btn btn-primary" style="submit" @click="create">Create</button>
      </div>
    </div>
    <div class="card mt-3">
      <div class="card-body col-12">
        <div class="d-flex justify-content-between">
          <h3>Todo List</h3>
          <button type="button" class="btn btn-primary" style="submit" @click="read">Read</button>
        </div>
        <table class="table table-borderless">
          <tr>
            <th>Name</th>
            <th>Description</th>
            <th>Deadline</th>
            <th></th>
          </tr>
          <tr v-for="todo in todos" :key="todo.name">
            <td height="60">{{ todo.name }}</td>
            <td>{{ todo.description }}</td>
            <td>{{ todo.deadline }}</td>
            <td><button type="btn btn-outline-primary button" class="btn-sm" style="submit" @click="deleteTodo(todo)">Delete</button></td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data: () => ({
    todos: [],
    todo:{
      name: "",
      description: "",
      deadline: ""
    },
    name: "todos"
  }),
  methods: {
    read() {
      const data = sessionStorage.getItem(this.name)
      if (data) {
        this.todos = JSON.parse(data)
      } 
    },
    create() {
      this.todos.push(this.todo)
      sessionStorage.setItem(this.name, JSON.stringify(this.todos))
      this.todo = {
        name: "",
        description: "",
        deadline: ""
      }
    },
    deleteTodo(todo) {
      //名前が一致しないものだけを取得
      this.todos = this.todos.filter((item) => item.name !== todo.name)
      sessionStorage.setItem(this.name, JSON.stringify(this.todos))
    },
    deleteAll() {
      sessionStorage.clear()
      this.todos =[]
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
