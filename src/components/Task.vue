<template>
    <div @dblclick="$emit('toggleDelete', task.id)" class="task" :style="{borderLeft: task.reminder ? '5px solid green': ''}">
        <h3 :style="{color: task.reminder ? 'green': 'yellow'}">{{task.text}}</h3>
        <i @click="$emit('deleteTask', task.id)" class="fas fa-times"></i>
        <p>{{task.day}}</p>
    </div>
</template>

<script>
export default {
    name: "Task",
    props: {
        task: Object
    }
}
</script>

<style scoped>
.fas {
  color: red;
}

.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>