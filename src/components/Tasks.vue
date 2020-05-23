<template>
    <div>
        <ul>
          <li v-for="task in tasks" :key="task.id">
            <input type="checkbox" @click="updateTaskStatus(task)" :checked="task.completed">
            <span v-show="editMode === task.id">
              <input type="text" class="form-control" v-model="task.title" placeholder="Name of the task">
            </span>
            <span v-show="editMode != task.id">
              <span :class="{ 'is-completed': task.completed }"> {{ task.title }} </span>
            </span>
            <span v-show="editMode === task.id">
              <button class="btn btn-success" @click="updateTask(task)">
                Save
              </button>
              <button class="btn btn-default" @click="cancelEdit(task)">
                Cancel
              </button>
            </span>
            <span v-show="editMode != task.id">
              <button class="btn btn-info" @click="setEditMode(task)">
                Edit
              </button>
              <button class="btn btn-danger" @click="$emit('delete:task', task.id)">
                Delete
              </button>
            </span>
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
    data: function() {
    return {
        editMode: '',
        oldData: ''
      }
    },
    methods: {
        updateTaskStatus: function (task) {
            task.completed = !task.completed
        },
        setEditMode: function (task) {
            this.editMode = task.id
            this.oldData = JSON.parse(JSON.stringify(task))
        },
        updateTask: function (task) {
            if (task.title === '') {
                return false
            }
            //Send to parent component
            this.$emit('update:task', task.id, task)
            this.editMode = null
        },
        cancelEdit: function (task) {
            task.title = this.oldData.title
            this.editMode = null
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
  width: 100%;
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

.btn-info {
    background-color: #007bff;
    border: 2px solid #007bff;
}

.btn-success {
    background-color: #41b883;
    border: 2px solid #41b883;
}
</style>