<template>
    <div>
      <h2>Edit Student</h2>
      <form @submit.prevent="updateStudent">
        <div>
          <label for="edit-name">Name:</label>
          <input type="text" id="edit-name" v-model="editedStudent.name" required>
        </div>
        <div>
          <label for="edit-email">Email:</label>
          <input type="email" id="edit-email" v-model="editedStudent.email" required>
        </div>
        <button type="submit">Update</button>
      </form>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      student: Object, // The student object passed from the controller
    },
    data() {
      return {
        editedStudent: {
          name: '',
          email: '',
        },
      };
    },
    created() {
      this.editedStudent = { ...this.student };
    },
    methods: {
      async updateStudent() {
        try {
          const response = await this.$inertia.put(`/students/${this.student.id}`, this.editedStudent);
          // Optionally, you can show a success message or handle other actions here.
        } catch (error) {
          // Handle error, show validation errors, etc.
        }
      },
    },
  };
  </script>
  