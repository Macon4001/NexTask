<template>
    <nav class="navbar">
      <div class="nav-logo-container">
        <img src="/images/2.png" alt="NexTask Logo" class="logo" />
        <img src="/images/NexTask.png" alt="NexTask Text Logo" class="logo-text" />
      </div>
      <ul class="nav-links">
        <li v-for="(link, index) in navLinks" :key="index" class="nav-link-item">
          <a :href="link.href" class="nav-link">{{ link.text }}</a>
          <span v-if="index < navLinks.length - 1" class="divider">|</span>
        </li>
        <!-- Add profile picture here -->
        <li class="nav-link-item profile-picture">
          <img src="/images/PP.png" alt="Profile Picture" class="profile-pic" />
        </li>
      </ul>
    </nav>
  </template>
  
  <script>
  export default {
    name: 'Nav',
    data() {
      return {
        navLinks: [
          { text: 'Home', href: '/' },
          { text: 'Dashboard', href: '/dashboard' },
          { text: 'Profile', href: '/profile' },
          { text: 'Tasks', href: '/tasks' },
        ],
      };
    },
  };
  </script>
  
  <style scoped>
  .navbar {
    width: 100%; /* Ensures full page width */
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0px 100px; /* Adjusted padding for a thinner look */
    background-color: #f9f9f9;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  }
  
  .nav-logo-container {
    display: flex;
    align-items: center;
    gap: 10px; /* Adds space between the two logos */
  }
  
  .logo {
    width: 60px; /* Adjust size as needed */
    height: auto;
  }
  
  .logo-text {
    width: 120px; /* Adjust size as needed */
    height: auto;
  }
  
  .nav-links {
    display: flex;
    list-style: none;
    padding: 0;
    margin: 0;
    align-items: center;
  }
  
  .nav-link-item {
    display: flex;
    align-items: center;
  }
  
  .nav-link {
    text-decoration: none;
    color: #333;
    font-size: 16px;
    font-weight: 500;
    transition: color 0.3s;
  }
  
  .nav-link:hover {
    color: #4CAF50; /* Change this color for a hover effect */
  }
  
  .divider {
    margin: 0 10px;
    color: #888; /* Subtle color for the divider */
  }
  
  .profile-pic {
    width: 40px; /* Adjust size as needed */
    height: 40px; /* Adjust size as needed */
    border-radius: 50%; /* Makes the image circular */
    margin-left: 20px; /* Adds spacing to the left */
    transition: border 0.3s; /* Adds smooth transition for hover effect */
  }
  
  .profile-pic:hover {
    border: 2px solid #4CAF50; /* Green outline on hover */
  }
  </style>
  