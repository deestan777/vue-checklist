<template>
  <div id="app">
    <h1 class="mt-3">Задачи</h1>
    <div class="container">
      <section>
        <div class="row justify-content-center mt-4">
          <input
              v-model="inputField"
              class="mr-1"
              placeholder="Название задачи"
              v-on:keyup.enter="addTodo"
          />
          <button class="btn btn-secondary" @click="addTodo">Добавить</button>
        </div>
      </section>

      <section class="container">
        <div class="row">
          <div class="offset-md-3 col-md-6 mt-3">
            <ul class="list-group justify-content-center">
              <li
                  v-for="todo in todoList"
                  :key="todo.name"
                  class="row list-group-item border mt-2 col-xs-1"
              >
                <div class="row align-items-center">
                  <input
                      class="col-sm-1 border border-danger"
                      type="checkbox"
                      v-bind:checked="todo.complete"
                      v-on:change="toggle(todo)"
                  />
                  <del v-if="todo.complete" class="col-sm-8">
                    <h5>{{ todo.name }}</h5>
                  </del>
                  <span v-else class="col-sm-8">
                    <h5>{{ todo.name }}</h5>
                  </span>
                  <span
                      class="offset-sm-1 col-sm-2 delete text-right"
                      @click="deleteTodo(todo)"
                  >X</span
                  >
                </div>
              </li>
            </ul>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import "bootstrap/dist/css/bootstrap.css";
import "bootstrap-vue/dist/bootstrap-vue.css";

export default {
  name: "app",
  methods: {
    addTodo: function (todo) {
      todo = this.inputField;
      if (todo == "") {
        alert("Введите название");
      } else if (todo.length <= 3) {
        alert('Короткое название')
      } else if (todo !== "" && todo.length >= 3) {
        this.todoList.push({name: todo, complete: false});
        this.inputField = "";
      }
    },
    deleteTodo: function (todo) {
      let index = this.todoList.indexOf(todo);
      this.todoList.splice(index, 1);
    },
    toggle: function (todo) {
      todo.complete = !todo.complete;
    },
  },
  data() {
    return {
      inputField: "",
      todoList: [],
    };
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

h5 {
  margin-bottom: 0px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.delete {
  color: pink;
  cursor: pointer;
}

.delete:hover {
  color: red;
}
</style>
