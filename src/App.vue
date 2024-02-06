<template>
  <div class="container">
    <Header title="Tasks Tracker" />
    <AddTask @add-task="addTask"/>
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
      tasks: []
    }
  },
  created() {
      this.tasks = [
      {
        "id": 1,
        "text": "Buy groceries",
        "day": "2024-02-10",
        "reminder": true
      },
      {
        "id": 2,
        "text": "Meeting with client",
        "day": "2024-02-15",
        "reminder": false
      },
      {
        "id": 3,
        "text": "Complete project",
        "day": "2024-03-01",
        "reminder": true
      },
      {
        "id": 4,
        "text": "Exercise",
        "day": "2024-02-12",
        "reminder": true
      },
      {
        "id": 5,
        "text": "Read a book",
        "day": "2024-02-20",
        "reminder": false
      }
]
  },
  methods: {
    handleDelete(id) {
      this.tasks = this.tasks.filter(task => task.id !== id)
    },
    handleToggle(id) {
      var task = this.tasks.find(task => task.id == id)
      task.reminder = !task.reminder

      console.log(task.reminder)
      // console.log(id)
    },
    addTask(task) {
      this.tasks.push(task)
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
  max-width: 500px;
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
