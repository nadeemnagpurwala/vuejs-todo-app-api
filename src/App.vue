<template>
  <div id="app">
    <Tasks :title="title" :tasks="tasks"/>
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
  padding: 0 1rem;
  color: #fff;
}

body {
  background: #32475f;
}
</style>
