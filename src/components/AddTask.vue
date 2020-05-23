<template>
    <div>
        <button class="btn btn-primary" @click="showAddForm()" v-show="!showForm">+ Add New Task</button>
        <form @submit.prevent="addTask" v-show="showForm" class="form">
            <input type="text" class="form-control" v-model="title" placeholder="Name of the task">
            <input type="submit" class="btn btn-success" value="Submit">
            <button class="btn btn-default" @click="hideAddForm()">Cancel</button>
        </form>
    </div>
</template>

<script>
export default {
    name:"AddTask",
    data: function() {
        return {
            showForm: false,
            title: ''
        }
    },
    methods: {
        showAddForm: function () {
            this.showForm = true
        },
        hideAddForm: function () {
            this.showForm = false
            this.title = ''
        },
        addTask: function () {
            if(this.title === ''){
                return false
            }
            const newTask = {
                title : this.title,
                completed : false
            }
            //Send to parent component
            this.$emit('add:task', newTask)
            this.title = ""
            this.showForm = false
        }
    }
}
</script>

<style scoped>
.form {
    margin-bottom: 50px;
}

.form-control {
  display: inline-block;
  padding: 10px 2px;
  font-size: 14px;
  width: 100%;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin: auto;
  margin-bottom: 10px;
}

.btn-success {
    background-color: #41b883;
    border: 2px solid #41b883;
    float: right;
}

.btn-primary {
    background-color: #41b883;
    border: 2px solid #41b883;
    width: 100%;
    margin: auto;
}

.btn-default {
    float: right;
}
</style>