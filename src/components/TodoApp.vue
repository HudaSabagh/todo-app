<template>
  <div class="container">
    <h1 class="text-center m-4">Todo App</h1>
    <div class="d-flex text-center nn">
      <input
        v-model="todo"
        type="text"
        placeholder="ENTER TASK"
        class="form-control"
      />
      <button class="btn btn-info rounded-1 mx-1" @click="handleInput">
        Add
      </button>
    </div>
    <div class="alert alert-danger my-2" role="alert" id="show">
      Please Enter your Task
    </div>
    <table class="table table-responsive">
      <thead class="table-light">
        <tr>
          <th>ToDO</th>
          <th>Status</th>
          <th>Edit</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td>{{ todo.name }}</td>
          <td>{{ todo.status }}</td>
          <td @click="editTodo(index)">
            <i class="fa fa-edit text-secondary"></i>
          </td>
          <td @click="removeTodo(index)">
            <i class="fa fa-remove text-danger"></i>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "TodoApp",
  data() {
    return {
      todo: "",
      editValue: null,
      todos: [
        { name: "kauf Apfel from Hofer es git ein Angebot ", status: "to-do" },
        { name: "lehrn vue JS ", status: "done" },
      ],
    };
  },
  methods: {
    handleInput() {
      if (this.todo.length === 0) {
        alert("Bitte Todo eintragen");
        document.querySelector("input").focus();

        /*   document.getElementById("show").style.display = "block"; */ //her ich habe ein frage warum display nicht diese msg?
      } else {
        if (this.editValue === null) {
          this.todos.push({
            name: this.todo,
            status: "to-do",
          });
        } else {
          this.todos[this.editValue].name = this.todo; //to avoid add new task instead of update it
          this.editValue = null; //to can add new task
        }
        this.todo = ""; //to clean input field
      }
    },
    removeTodo(index) {
      this.todos.splice(index, 1); //splice(from this index remove,number of the item which we want to remove it)
    },
    editTodo(index) {
      this.todo = this.todos[index].name;
      this.editValue = index; //to update this todo with this index not add new one
    },
  },
};
</script>
<style scoped>
.fa {
  cursor: pointer;
}
#show {
  display: none;
}
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
