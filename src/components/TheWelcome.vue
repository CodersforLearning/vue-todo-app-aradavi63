<template>
  <div class="addTaskBox">
    <form id="taskForm" @submit.prevent="addTask">
      <h2>To Do List</h2>
      <input type="text" id="taskName" v-model="newTask" placeholder="Name of task">
      <input type="submit" id="addTask" value="Add!">
    </form>
    <ul class="toDoList">
      <li v-for="(task, index) in tasks" :key="index" :class="{ completed: task.completed }">
        <span>{{ task.name }}</span>
        <div>
          <button @click="markAsCompleted(index)">
            {{ task.completed ? "Undo" : "Completed" }}
          </button>
          <button @click="removeTask(index)">Remove</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/*.addTaskBox {
  background-color: #cdeccb;
  height: 200px;
  width: 600px;
  border: 10px #090011;
  border-radius: 8px;
  margin: 10px; 
  padding: 20px;
}*/

.addTaskBox {
  width: 600px;
  margin: 0 auto; 
  text-align: center;
  font-family: Arial, sans-serif;
  padding: 20px; 
  background-color: #cdeccb; /* Light background for contrast */
  border: solid 2px #333c46;
  border-radius: 8px; /* Rounded corners */
}


input[type="text"] {
  width: 70%;
  padding: 8px;
  margin: 10px 0;
}

input[type="submit"] {
  padding: 8px 16px;
  cursor: pointer;
  
}

.toDoList {
  background-color: #cdeccb;
  list-style-type: none;
  padding: 0;
}

.toDoList li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 3px;
  padding: 8px;
  border: solid 1px #283e59;
}

.toDoList li.completed {
  text-decoration: line-through;
  color: gray;
  background-color: #babdba;
}

.toDoList button {
  background: #007bff;
  color: white;
  border: none;
  padding: 4px 8px;
  margin-left: 5px;
  cursor: pointer;
}

.toDoList button:hover {
  background: #0056b3;
}

.toDoList button:last-child {
  background: red;
}

.toDoList button:last-child:hover {
  background: darkred;
}
</style>

<script>
export default {
  data() {
    return {
      newTask: '', // Holds the value of the input field
      tasks: []    // Array to store tasks
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ name: this.newTask.trim(), completed: false }); // Add task with completed status
        this.newTask = ''; // Clear the input field
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1); // Remove the task at the specified index
    },
    markAsCompleted(index) {
      this.tasks[index].completed = !this.tasks[index].completed; // Toggle completed status
    }
  }
};
</script>
