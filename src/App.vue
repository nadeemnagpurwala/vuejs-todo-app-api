<template>
  <div id="app">
    <div :class="{ 'loader': loading }"></div>
    <Tasks :title="title" :tasks="tasks" @delete:task="deleteTask"/>
  </div>
</template>

<script>
import Tasks from './components/Tasks.vue'

export default {
  name: 'App',
  components: {
    Tasks
  },
  data: function() {
    return {
      title: 'Tasks for the day',
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
            'https://jsonplaceholder.typicode.com/todos?_limit=5'
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
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 450px;
  margin: 2rem auto;
  color: #222;
  padding: 15px;
  background-color: #fff;
  border-radius: .5rem;
}

body {
  background: #32475f;
}

button {
  cursor: pointer;
  background: #888181;
  color: #fff;
  border: 2px solid #888181;
  margin: 0 .5rem;
}

.form-control, button {
  display: inline-block;
  -webkit-appearance: none;
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
  opacity: 0.5;
}
</style>
