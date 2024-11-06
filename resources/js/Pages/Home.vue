<template>
          <Nav /> 
    <div class="home-container">
      <header class="header">
      </header>
      
      <main class="main-content">
        <div v-if="tasks.length === 0" class="empty-state">
          <p>You have no tasks yet. Start by creating one!</p>
          <button @click="createTask" class="btn-primary">Create New Task</button>
        </div>
        <ul v-else class="task-list">
          <li v-for="task in tasks" :key="task.id" class="task-item">
            <h3>{{ task.title }}</h3>
            <p>{{ task.description }}</p>
          </li>
        </ul>
      </main>
    </div>
   <Footer />
  </template>
  
  <script>
  import Nav from './Nav.vue'; 
  import Footer from './Footer.vue'

  export default {
    components: {
      Nav, // Register the Nav component
      Footer,
    },
    data() {
      return {
        tasks: [
          // Replace with task data fetched from your API or store
          { id: 1, title: 'Example Task 1', description: 'This is an example task.' },
          { id: 2, title: 'Example Task 2', description: 'This is another task.' }
        ]
      };
    },
    methods: {
      createTask() {
        // Navigate to a task creation page or open a task creation modal
        alert('Navigate to create task functionality');
      }
    }
  };
  </script>
  
  <style scoped>
  .logo {
    width: 100px; /* Adjust as needed */
    height: auto;
  }
  
  .home-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 20px;
    font-family: 'Arial', sans-serif;
  }
  
  .header {
    text-align: left;
    margin-bottom: 20px;
  }
  
  .subtitle {
    color: #888;
  }
  
  .main-content {
    background: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }
  
  .empty-state {
    text-align: center;
    color: #555;
  }
  
  .btn-primary {
    background-color: #4CAF50;
    color: #fff;
    border: none;
    padding: 10px 20px;
    margin-top: 10px;
    cursor: pointer;
    border-radius: 4px;
    transition: background-color 0.3s;
  }
  
  .btn-primary:hover {
    background-color: #45a049;
  }
  
  .task-list {
    list-style: none;
    padding: 0;
  }
  
  .task-item {
    background: #fff;
    padding: 15px;
    margin-bottom: 10px;
    border-radius: 8px;
    box-shadow: 0 1px 5px rgba(0, 0, 0, 0.1);
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
  