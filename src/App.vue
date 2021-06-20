<template>
  <Tasks :todoList="todoList" 
          @getLimitedTodos="getLimitedTodos" 
          @filterTodo="filterTodo"
          @markAsCompleted="markAsCompleted"
          @addNewTask = "addNewTask"
          />
</template>

<script>
import Tasks from './components/Tasks.vue'

export default {
  name: 'App',
  data() {
    return {
      todoList: []
    }
  },
  methods: {
    async getTaskList (){
      const res = await fetch('https://jsonplaceholder.typicode.com/todos');
      const data = await res.json();
      return data;
    },

    async getLimitedTodos(limit) {
      if (limit) {
        const res = await fetch(`https://jsonplaceholder.typicode.com/todos?_limit=${limit}`);
        const data = await res.json();
        this.todoList = data;
      }else {
        this.todoList = await this.getTaskList();
      }
    },

    async filterTodo(filterText) {
      if (filterText) {
        this.todoList = this.todoList.filter( todo => todo.title.includes(filterText));
      }else {
        this.todoList = await this.getTaskList();
      }
    },

    markAsCompleted(id) {
      this.todoList = this.todoList.map(todo => {
        if (todo.id == id) {
          return {...todo, completed: true}
        }
        return todo;
      })
    }, 
    addNewTask(newTask) {
      this.todoList.unshift(newTask)
    }
  },
  components: {
    Tasks
  },
  async created() {
    this.todoList = await this.getTaskList();
  }
}
</script>

<style>

</style>
