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
    <div class="alert alert-danger my-2 d-none" role="alert" id="show">
      Please Enter your Task
    </div>
    <table class="table table-responsive">
      <thead class="table-light">
        <tr>
          <th style="width: 300px">ToDO</th>
          <th>Status</th>
          <th>Edit</th>
          <th>Delete</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todos" :key="index">
          <td style="width: 300px">
            <span
              :class="{
                'text-decoration-line-through': todo.status === 'Finished',
              }"
              >{{ todo.name }}</span
            >
          </td>
          <td>
            <span
              @click="changeStatus(index)"
              id="status"
              :class="{
                'text-danger': todo.status === 'Todo',
                'text-warning': todo.status === 'In progress',
                'text-success': todo.status === 'Finished',
              }"
              >{{ todo.status }}</span
            >
          </td>
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
      statusAvailable: ["Todo", "In progress", "Finished"],
      todos: [
        { name: "kauf Apfel from Hofer es git ein Angebot ", status: "Todo" },
        { name: "lehrn vue JS ", status: "In progress" },
        { name: "lehrn HTML ", status: "Finished" },
      ],
    };
  },
  methods: {
    changeStatus(index) {
      let newIndex = this.statusAvailable.indexOf(this.todos[index].status);

      if (++newIndex > 2) newIndex = 0; //our array hat 0 1 2 index when greater als 2 then put it 0

      this.todos[index].status = this.statusAvailable[newIndex];
    },
    handleInput() {
      if (this.todo.length === 0) {
        alert("Bitte Todo eintragen");
        document.querySelector("input").focus();

        /*    document.getElementById("show").style.display = "block";  */ //her ich habe ein frage warum display nicht diese msg?
      } else {
        if (this.editValue === null) {
          this.todos.push({
            name: this.todo,
            status: "Todo",
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
#status {
  cursor: pointer;
  font-weight: bold;
}
.finished {
  text-decoration: line-through;
}
td,
th {
  width: 120px;
}
</style>

<!-- Add "scoped" attribute to limit CSS to this component only -->
