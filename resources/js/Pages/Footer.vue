<template>
    <footer class="footer">
      <div class="footer-content">
        <div class="footer-logo">
          <img src="/images/NexTask (1).png" alt="NexTask Logo" class="logo" />
        </div>
        <div class="footer-section">
          <p>&copy; 2024 NexTask. All rights reserved.</p>
        </div>
        <div class="footer-section links">
          <a href="/terms" class="footer-link">Terms of Service</a>
          <span class="divider">|</span>
          <a href="/privacy" class="footer-link">Privacy Policy</a>
        </div>
        <div class="footer-section social">
          <p>Follow me:</p>
          <div class="social-links">
            <a href="https://github.com/Macon4001" target="_blank" class="social-link">
              <img src="/images/github.png" alt="GitHub" class="icon" />
            </a>
            <span class="divider">|</span>
            <a href="https://www.linkedin.com/in/michael-muniu-135a54200/" target="_blank" class="social-link">
              <img src="/images/linkedin.png" alt="LinkedIn" class="icon" />
            </a>
          </div>
        </div>
      </div>
    </footer>
  </template>
  
  <script>
  export default {
    name: 'Footer',
  };
  </script>
  
  <style scoped>
  .footer {
    background-color: #f1f1f1;
    padding: 20px 30px;
    border-top: 1px solid #ddd;
    font-family: 'Arial', sans-serif;
    color: #333;
  }
  
  .footer-content {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    max-width: 100%;
    margin: 0 auto;
    gap: 20px;
  }
  
  .footer-logo {
    flex: 1;
  }
  
  .logo {
    width: 120px; /* Adjust size as needed */
    height: auto;
  }
  
  .footer-section {
    text-align: left;
    flex: 5;
  }
  
  .links {
    flex: 2;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .social {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .social-links {
    display: flex;
    align-items: center;
    gap: 5px; /* Space between icons */
  }
  
  .icon {
    width: 24px; /* Adjust the icon size */
    height: auto;
  }
  
  .footer-link {
    color: #007BFF;
    text-decoration: none;
    margin: 0 5px;
    font-weight: 500;
  }
  
  .footer-link:hover {
    text-decoration: underline;
  }
  
  .divider {
    margin: 0 5px;
    color: #555;
  }
  
  .social-link:hover {
    color: #4CAF50;
  }
  </style>
  