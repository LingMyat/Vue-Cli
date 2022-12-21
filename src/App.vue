<template>
  <div class="container">
    <div class="row pt-4">
      <div class="col-md-5 col-12 mb-3">
        <div class="card shadow">
          <div class="card-header">
            <h3>{{ title1 }}</h3>
          </div>
          <div class="card-body">
            <div class="input-group">
              <input type="text" v-model="inputTask" class="form-control" />
              <button
                @click="addTodo"
                class="btn btn-secondary"
                :disabled="inputTask === ''"
              >
                Add+
              </button>
            </div>
          </div>
        </div>
      </div>
      <div class="col-md-7 col-12">
        <div class="card shadow">
          <div class="card-header">
            <h3>{{ title2 }}</h3>
          </div>
          <div class="card-body">
            <div class="">
              <i
                ><b>{{ text }}</b></i
              >
            </div>
            <div v-for="(todo, index) in todos" :key="index">
              <div class="d-flex gap-1">
                <input type="checkbox" v-model="todo.done" id="" />
                <span :class="{ done: todo.done }" class="d-inline-block"
                  ><i>
                    {{ todo.task }}
                  </i></span
                >
                <button @click="deleteTodo(index)" class="btn btn-sm btn-danger" :disabled="!todo.done">
                  <i class="fa-solid fa-xmark"></i>
                </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    title1: "Add Your Tasks",
    title2: "My Tasks",
    inputTask: "",
    todos: [],
  }),
  methods: {
    addTodo() {
      this.todos.push({
        task: this.inputTask,
        done: false,
      });
      this.setDefault();
    },
    deleteTodo(index){
      this.todos.splice(index,1);
    },
    setDefault() {
      this.inputTask = "";
    },
  },
  computed: {
    text() {
      if (this.todos.length == 0) {
        return "There is no task here";
      }
      return "";
    },
  },
};
</script>

<style>
* {
  user-select: none;
}
.done {
  text-decoration: line-through;
}
</style>
