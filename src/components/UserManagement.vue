<template>
    <div>
      <h1>User Management</h1>
      <form @submit.prevent="createUser">
        <label for="name">Name:</label>
        <input type="text" id="name" v-model="userData.name" required>
        <br>
        <label for="email">Email:</label>
        <input type="email" id="email" v-model="userData.email" required>
        <br>
        <label for="gender">Gender:</label>
        <select id="gender" v-model="userData.gender" required>
          <option value="male">Male</option>
          <option value="female">Female</option>
        </select>
        <br>
        <label for="address">Address:</label>
        <textarea id="address" v-model="userData.address" required></textarea>
        <br>
        <button type="submit">Create User</button>
      </form>
      <div v-if="error" class="error-message">{{ error }}</div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        userData: {
          name: '',
          email: '',
          gender: '',
          address: ''
        },
        error: ''
      };
    },
    methods: {
      async createUser() {
        try {
          const response = await fetch('http://localhost:8080/api/users', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify(this.userData)
          });
          if (!response.ok) {
            throw new Error('Failed to create user');
          }
          alert('User created successfully');
          this.userData = {
            name: '',
            email: '',
            gender: '',
            address: ''
          };
        } catch (error) {
          this.error = error.message;
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .error-message {
    color: red;
  }
  </style>
  