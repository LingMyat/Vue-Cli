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
              <input type="text" v-model="inputTask" @change="addTodo" class="form-control" />
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
          <div class="card-body" >
            <div class="" v-if="filterTasks.length == 0">
              <i
                ><b>There is no task here</b></i
              >
            </div>
            <div v-for="(todo, index) in filterTasks" :key="index" v-else>
              <div class="d-flex gap-1 mb-2">
                <input type="checkbox" v-model="todo.done" id="" @change="storeTodos"/>
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
          <div class="card-footer">
            <b><i>Hide Complete Tasks</i></b> <input type="checkbox" v-model="hideCompleteTasks">
            <button class="btn btn-sm btn-primary float-end">Delete Complete Tasks</button>
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
    hideCompleteTasks:false,
    todos: [],
  }),
  methods: {
    addTodo() {
      this.todos.push({
        task: this.inputTask,
        done: false,
      });
      this.storeTodos();
      this.setDefault();
    },
    deleteTodo(index){
      this.todos.splice(index,1);
      this.storeTodos();
      
    },
    setDefault() {
      this.inputTask = "";
    },
    storeTodos(){
      localStorage.setItem('todoList',JSON.stringify(this.todos));
    }
  },
  mounted(){
    localStorage.getItem('todoList')==null?this.todos=[]:this.todos=JSON.parse(localStorage.getItem('todoList'));
  },
  computed: {
    filterTasks(){
      // return this.hideCompleteTasks? this.todos.filter((v)=>!v.done) : this.todos;
      if (this.hideCompleteTasks) {
        let filterArr =  this.todos.filter(function(e){
              return e.done == false;
          });
          return filterArr;
      }
      return this.todos;
    }
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
