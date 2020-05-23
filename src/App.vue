<template>
  <div id="app">
    <h1 class="heading">{{ title }}</h1>
    <div class="main-section">
      <div :class="{ 'loader': loading }"></div>
      <AddTask @add:task="addTask"/>
      <Tasks :tasks="tasks" @delete:task="deleteTask"/>
    </div>
  </div>
</template>

<script>
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Tasks,
    AddTask
  },
  data: function() {
    return {
      title: 'Todo List App',
      loading: false,
      tasks:[],
    }
  },
  mounted() {
    this.getTasks()
  },
  methods: {
    async getTasks() {
      try {
          const response = await fetch(
            'https://jsonplaceholder.typicode.com/todos?_limit=3'
          )
          const data = await response.json()
          this.tasks = data
        }
      catch (error) {
          console.error(error)
      }
    },
    async deleteTask(id) {
      this.loading = true
      try {
        await fetch(`https://jsonplaceholder.typicode.com/todos/${id}`, {
          method: "DELETE"
        })
        this.tasks = this.tasks.filter(
          task => task.id !== id
        )
        this.loading = false
      }
      catch (error) {
        console.error(error);
      }
    },
    async addTask(newTask) {
      this.loading = true
      try {
        const response = await fetch('https://jsonplaceholder.typicode.com/todos', {
          method: 'POST',
          body: JSON.stringify(newTask),
          headers: { 'Content-type': 'application/json; charset=UTF-8' },
        })
        const data = await response.json()
        this.tasks = [...this.tasks, data]
        this.loading = false
      } catch (error) {
        console.error(error)
      }
    }
  }
}
</script>

<style>
body {
  background: #32475f;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.heading {
  text-align: center;
  color: #fff;
}

.main-section {
  max-width: 500px;
  margin: 2rem auto;
  color: #222;
  padding: 15px;
  background-color: #fff;
  border-radius: .5rem;
}

.btn {
  cursor: pointer;
  background: #888181;
  color: #fff;
  border: 2px solid #888181;
  margin: 0 .5rem;
  display: inline-block;
  padding: .5rem 1rem;
  border-radius: 4px;
}

.loader{
  position: fixed;
  left: 0px;
  top: 0px;
  width: 100%;
  height: 100%;
  background: url('../public/loader.gif') 50% 50% no-repeat rgb(249,249,249);
  background-size: 50px;
  opacity: 0.5;
}
</style>
