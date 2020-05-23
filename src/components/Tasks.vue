<template>
    <div>
        <ul>
          <li v-for="task in tasks" :key="task.id">
            <input type="checkbox" @click="updateTaskStatus(task)" :checked="task.completed">
            <span :class="{ 'is-completed': task.completed }">{{ task.title }}</span>
            <button class="btn btn-danger" @click="$emit('delete:task', task.id)">
              Delete
            </button>
          </li>
        </ul>
    </div>
</template>

<script>
export default {
    name:"Tasks",
    props: {
        tasks: Array
    },
    methods: {
        updateTaskStatus: function (task) {
            task.completed = !task.completed
        }
    }
}
</script>

<style scoped>
ul {
  padding: 0;
}

li {
  display: flex;
  align-items: center;
  padding: .5rem;
  margin-bottom: 1rem;
}

li span {
  display: inline-block;
  padding: .5rem;
  width: 300px;
  border-radius: 4px;
  border: 2px solid transparent;
}

[type="checkbox"] {
  margin-right: 1rem;
}

.is-completed {
  text-decoration: line-through;
  color: #ccc;
}

.btn-danger {
  background-color: #dc3545;
  border: 2px solid #dc3545;
}
</style>