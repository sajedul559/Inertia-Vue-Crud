<template>
    <div>
      <h2>Create Student</h2>
      <form @submit.prevent="createStudent">
        <div>
          <label for="name">Name:</label>
          <input type="text" id="name" v-model="student.name" required>
        </div>
        <div>
          <label for="email">Email:</label>
          <input type="email" id="email" v-model="student.email" required>
        </div>
        <button type="submit">Create</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        student: {
          name: '',
          email: '',
        },
      };
    },
    methods: {
      async createStudent() {
        try {
          const response = await this.$inertia.post('/students/create', this.student);
          // Optionally, you can show a success message or handle other actions here.
        } catch (error) {
          // Handle error, show validation errors, etc.
        }
      },
    },
  };
  </script>
  