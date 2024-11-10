<template>
  <Nav />
  <div class="home-container">
    <header class="header">
      <h1>Task Manager</h1>
    </header>

    <!-- Create Task Column -->
    <div class="task-column create-task-column" v-if="showTaskForm">
      <h2>Create New Task</h2>
      <div class="task-form">
        <input v-model="newTaskTitle" placeholder="Task Title" class="input-title" />
        <textarea v-model="newTaskDescription" placeholder="Task Description" class="input-description"></textarea>
        <input type="date" v-model="newTaskDeadline" class="input-deadline" />
        <select v-model="newTaskImportance" class="input-importance">
          <option value="1">!</option>
          <option value="2">!!</option>
          <option value="3">!!!</option>
        </select>
        <button @click="addTask" class="btn-add-task">Add Task</button>
      </div>
    </div>
    <button @click="showTaskForm = !showTaskForm" class="btn-create-task">
      {{ showTaskForm ? 'Cancel' : '+ New Task' }}
    </button>

    <main class="main-content">
      <!-- New Task Column -->
      <div class="task-column new-tasks" @dragover.prevent @drop="onDrop('newTasks')">
        <h2>New Tasks</h2>
        <div
          v-for="(task, index) in newTasks"
          :key="task.id"
          class="task-item task-item-new"
          draggable="true"
          @dragstart="onDragStart('newTasks', index)"
        >
          <div class="importance-indicator" :class="`importance-${task.importance}`">
            {{ getImportanceSymbol(task.importance) }}
          </div>
          <div class="task-content">
            <h3>{{ task.title }}</h3>
            <p>{{ task.description }}</p>
            <p class="task-deadline">Deadline: {{ task.deadline }}</p>
          </div>
          <button @click="deleteTask('newTasks', index)" class="btn-delete-task">Delete</button>
        </div>
      </div>

      <!-- In Progress Column -->
      <div class="task-column in-progress-tasks" @dragover.prevent @drop="onDrop('inProgressTasks')">
        <h2>In Progress</h2>
        <div
          v-for="(task, index) in inProgressTasks"
          :key="task.id"
          class="task-item task-item-in-progress"
          draggable="true"
          @dragstart="onDragStart('inProgressTasks', index)"
        >
          <div class="importance-indicator" :class="`importance-${task.importance}`">
            {{ getImportanceSymbol(task.importance) }}
          </div>
          <div class="task-content">
            <h3>{{ task.title }}</h3>
            <p>{{ task.description }}</p>
            <p class="task-deadline">Deadline: {{ task.deadline }}</p>
          </div>
          <button @click="deleteTask('inProgressTasks', index)" class="btn-delete-task">Delete</button>
        </div>
      </div>

      <!-- Completed Task Column -->
      <div class="task-column completed-tasks" @dragover.prevent @drop="onDrop('completedTasks')">
        <h2>Completed Tasks</h2>
        <div
          v-for="(task, index) in completedTasks"
          :key="task.id"
          class="task-item task-item-completed"
          draggable="true"
          @dragstart="onDragStart('completedTasks', index)"
        >
          <div class="importance-indicator" :class="`importance-${task.importance}`">
            {{ getImportanceSymbol(task.importance) }}
          </div>
          <div class="task-content">
            <h3>{{ task.title }}</h3>
            <p>{{ task.description }}</p>
            <p class="task-deadline">Deadline: {{ task.deadline }}</p>
          </div>
          <button @click="deleteTask('completedTasks', index)" class="btn-delete-task">Delete</button>
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
      showTaskForm: false,
      newTaskTitle: '',
      newTaskDescription: '',
      newTaskDeadline: '',
      newTaskImportance: '1',
      newTasks: [
        { id: 1, title: 'Task 1', description: 'This is a new task.', deadline: '2024-11-15', importance: '1' },
        { id: 4, title: 'Task 4', description: 'Another new task.', deadline: '2024-11-20', importance: '2' }
      ],
      inProgressTasks: [
        { id: 2, title: 'Task 2', description: 'This task is in progress.', deadline: '2024-11-18', importance: '2' }
      ],
      completedTasks: [
        { id: 3, title: 'Task 3', description: 'This task is completed.', deadline: '2024-11-10', importance: '3' }
      ],
      draggedTask: null,
      draggedFrom: '',
    };
  },
  methods: {
    addTask() {
      if (this.newTaskTitle.trim()) {
        this.newTasks.push({
          id: Date.now(),
          title: this.newTaskTitle,
          description: this.newTaskDescription,
          deadline: this.newTaskDeadline,
          importance: this.newTaskImportance,
        });
        this.newTaskTitle = '';
        this.newTaskDescription = '';
        this.newTaskDeadline = '';
        this.newTaskImportance = '1';
        this.showTaskForm = false;
      }
    },
    getImportanceSymbol(importance) {
      return importance === '1' ? '!' : importance === '2' ? '!!' : '!!!';
    },
    onDragStart(listName, index) {
      this.draggedTask = this[listName][index];
      this.draggedFrom = listName;
    },
    onDrop(targetListName) {
      if (this.draggedTask && this.draggedFrom !== targetListName) {
        this[this.draggedFrom] = this[this.draggedFrom].filter(
          (task) => task.id !== this.draggedTask.id
        );
        this[targetListName].push(this.draggedTask);
        this.draggedTask = null;
        this.draggedFrom = '';
      }
    },
    deleteTask(listName, index) {
      this[listName].splice(index, 1);
    },
  },
};
</script>
<style scoped>
.home-container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  color: #333;
}

.header {
  text-align: center;
  margin-bottom: 20px;
  font-size: 2rem;
}

.btn-create-task {
  margin-bottom: 20px;
  padding: 10px 20px;
  background-color: #4CAF50;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 8px;
  font-weight: 500;
  transition: background-color 0.3s;
}

.btn-create-task:hover {
  background-color: #45a049;
}

.create-task-column {
  background: #f9f9f9;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.1);
  margin-bottom: 20px;
}

.task-form {
  display: flex;
  flex-direction: column;
  gap: 12px;
}

.input-title,
.input-description, 
.input-deadline, 
.input-importance { 
  padding: 12px; 
  border: 1px solid #d1d1d1; 
  border-radius: 8px; 
  background-color: #fff; 
  outline: none; 
  font-size: 1rem; 
  transition: border-color 0.2s; 
}

.input-title,
.input-description,
.input-deadline,
.input-importance {
  border-color: #4CAF50;
}

.main-content {
  display: flex;
  justify-content: space-between;
  gap: 24px;
}

.task-column {
  flex: 1;
  background: #f0f0f0;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.task-item {
  background: #fff;
  padding: 15px;
  margin-bottom: 12px;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.05);
  border: 1px solid transparent;
  transition: border-color 0.2s;
  position: relative;
}

.task-item-new {
  border-color: #007aff;
}

.task-item-in-progress {
  border-color: #ff9500;
}

.task-item-completed {
  border-color: #34c759;
}

.importance-indicator {
  position: absolute;
  top: 8px;
  right: 8px;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  color: #fff;
  font-size: 0.75rem;
}

.importance-1 {
  background-color: #ffcc00;
}

.importance-2 {
  background-color: #ff9900;
}

.importance-3 {
  background-color: #ff3b30;
}

.task-item h3 {
  margin: 0 0 8px;
  font-size: 1.2rem;
}

.task-item p {
  margin: 0;
  font-size: 0.95rem;
  color: #555;
}

.task-deadline {
  font-size: 0.85rem;
  color: #888;
  margin-top: 8px;
}

.btn-delete-task {
  margin-top: 10px;
  padding: 5px 10px;
  background-color: #e74c3c;
  color: #fff;
  border: none;
  cursor: pointer;
  border-radius: 4px;
  font-size: 0.85rem;
  transition: background-color 0.2s;
}

.btn-delete-task:hover {
  background-color: #c0392b;
}
</style>
