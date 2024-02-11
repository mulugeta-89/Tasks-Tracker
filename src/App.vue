<template>
  <div class="container">
    <Header title="Tasks Tracker" @toggle-add-task="toggleAddTask" :showAddTask="showAddTask"/>
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggleTask="handleToggle" @deleteTask="handleDelete" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from "./components/Header"
import Tasks from "./components/Tasks.vue"
import AddTask from "./components/AddTask.vue"
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    }
  },
  async created() {
      this.tasks = await this.fetchTasks()
  },
  methods: {
    async handleDelete(id) {
      const res = await fetch(`http://localhost:5000/tasks/${id}`, {
        method: "DELETE"
      })
      
      if (res.status === 200) {
        this.tasks = this.tasks.filter(task => task.id !== id)
      } else {
        alert("Error has occurred")
      }
    },
    handleToggle(id) {
      var task = this.tasks.find(task => task.id == id)
      task.reminder = !task.reminder
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(task)
      })

      const data = await res.json()
      this.tasks.push(data)
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask
      console.log(this.showAddTask)
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json()
      return data
    }
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
}

.container {
  max-width: 700px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}

.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
