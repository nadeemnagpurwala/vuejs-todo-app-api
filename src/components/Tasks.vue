<template>
    <div>
        <h1>{{ title }}</h1>
        <ul>
          <li v-for="task in tasks" :key="task.id">
            <input type="checkbox">
            <span>{{ task.title }}</span>
          </li>
        </ul>
    </div>
</template>

<script>
export default {
    name:"Tasks",
    props: {
        title: String,
        tasks: Array,
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
  padding: 1rem;
  margin-bottom: 1rem;
  background: #f4f4f4;
  border-radius: .5rem;
  color: #222;
}

li span {
  display: inline-block;
  padding: .5rem;
  width: 250px;
  border-radius: 4px;
  border: 2px solid transparent;
}

[type="checkbox"] {
  margin-right: 1rem;
}
</style>