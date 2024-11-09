<template>
  <Nav />
  <div class="home-container">
    <header class="header">
      <h1>Task Manager</h1>
    </header>

    <main class="main-content">
      <!-- New Task Column -->
      <div class="task-column new-tasks" @dragover.prevent @drop="onDrop('newTasks')">
        <h2>New Tasks</h2>
        <div
          v-for="(task, index) in newTasks"
          :key="task.id"
          class="task-item"
          draggable="true"
          @dragstart="onDragStart('newTasks', index)"
        >
          <h3>{{ task.title }}</h3>
          <p>{{ task.description }}</p>
        </div>
      </div>

      <!-- In Progress Column -->
      <div class="task-column in-progress-tasks" @dragover.prevent @drop="onDrop('inProgressTasks')">
        <h2>In Progress</h2>
        <div
          v-for="(task, index) in inProgressTasks"
          :key="task.id"
          class="task-item"
          draggable="true"
          @dragstart="onDragStart('inProgressTasks', index)"
        >
          <h3>{{ task.title }}</h3>
          <p>{{ task.description }}</p>
        </div>
      </div>

      <!-- Completed Task Column -->
      <div class="task-column completed-tasks" @dragover.prevent @drop="onDrop('completedTasks')">
        <h2>Completed Tasks</h2>
        <div
          v-for="(task, index) in completedTasks"
          :key="task.id"
          class="task-item"
          draggable="true"
          @dragstart="onDragStart('completedTasks', index)"
        >
          <h3>{{ task.title }}</h3>
          <p>{{ task.description }}</p>
        </div>
      </div>
    </main>
  </div>
  <Footer />
</template>

<script>
import Nav from './Nav.vue';
import Footer from './Footer.vue';

export default {
  components: {
    Nav,
    Footer,
  },
  data() {
    return {
      newTasks: [
        { id: 1, title: 'Task 1', description: 'This is a new task.' },
        { id: 4, title: 'Task 4', description: 'Another new task.' }
      ],
      inProgressTasks: [
        { id: 2, title: 'Task 2', description: 'This task is in progress.' }
      ],
      completedTasks: [
        { id: 3, title: 'Task 3', description: 'This task is completed.' }
      ],
      draggedTask: null,
      draggedFrom: '',
    };
  },
  methods: {
    onDragStart(listName, index) {
      this.draggedTask = this[listName][index];
      this.draggedFrom = listName;
    },
    onDrop(targetListName) {
      if (this.draggedTask && this.draggedFrom !== targetListName) {
        // Remove task from original list
        this[this.draggedFrom] = this[this.draggedFrom].filter(
          (task) => task.id !== this.draggedTask.id
        );
        // Add task to new list
        this[targetListName].push(this.draggedTask);
        this.draggedTask = null;
        this.draggedFrom = '';
      }
    },
  },
};
</script>

<style scoped>
.home-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

.header {
  text-align: center;
  margin-bottom: 20px;
}

.main-content {
  display: flex;
  justify-content: space-between;
  gap: 20px; /* Space between columns */
}

.task-column {
  flex: 1;
  background: #f9f9f9;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  transition: outline 0.3s ease-in-out; /* Animation for outline */
}

.new-tasks .task-item {
  outline: 2px solid red;
}

.in-progress-tasks .task-item {
  outline: 2px solid orange;
}

.completed-tasks .task-item {
  outline: 2px solid green;
}

.task-item {
  background: #fff;
  padding: 15px;
  margin-bottom: 10px;
  border-radius: 8px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
  cursor: grab;
  transition: outline 3s ease-in-out; /* Animation for changing outline */
}

.task-item h3 {
  margin: 0;
  font-size: 1.2em;
}

.task-item p {
  margin: 5px 0 0;
  color: #666;
}
</style>
