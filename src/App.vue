<template>
  <div class="container">
    <h1>To-do list</h1>
    <ul>
      <ToDoList 
      :tasks="tasks" 
      @add-task-list="addTaskList"
      @del-task="delTask"
      @toggle-task="toggleTask"
      />
    </ul>
  </div>
</template>

<script>
import ToDoList from "./components/ToDoList.vue";
import { ref } from 'vue';

export default {
  name: 'App',
  components: { ToDoList },

  setup() {
    const tasks = ref([])

    const addTaskList = (task) => {
      tasks.value.push({
        id: tasks.value.length + 1,
        text: task,
        completed: false,
    })
    }

    const delTask = (taskId) => {
      tasks.value = tasks.value.filter((task) => task.id !== taskId)
    }

    const toggleTask = (task) =>{
      task.completed = !task.completed
    }

    return { tasks, addTaskList, delTask, toggleTask }
  },
}

</script>

<style scoped>
  .container {
      max-width: 70vw;
      text-align: center;
      margin: 0 auto;
      background: linear-gradient(#4d4ddbad, 50%, #ff94a7);
      border-radius: 15px;
      padding: 10px;
      box-shadow: 0 4px 8px rgba(4, 4, 6, 0.3);
  }

  h1 {
      color: white;
      font-size: xxx-large;
  }

  ul {
    max-width: 52vw;
    color: white;
    font-size: 15px;
    list-style-type: none;
    margin: 0 auto;
    padding: 0;
}
</style>
