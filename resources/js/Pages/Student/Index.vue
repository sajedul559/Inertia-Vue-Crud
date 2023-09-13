<template>
    <div class="content">
      <router-view></router-view>

      <h1>Student List</h1><br>
      <router-link :to="{ name: 'students.create' }">Create Student</router-link>


      <table>
        <thead>
          <tr>
            <th>Name</th>
            <th>Email</th>
            <th>Actions</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="student in students" :key="student.id">
            <td>{{ student.name }}</td>
            <td>{{ student.email }}</td>
            <td>
              <button @click="editStudent(student)">Edit</button>
              <button @click="deleteStudent(student.id)">Delete</button>
            </td>
          </tr>
        </tbody>
      </table>
      <!-- Edit Student Form -->
    <div v-if="editingStudent">
      <h2>Edit Student</h2> <br>

      <form @submit.prevent="updateStudent">
        <div>
          <label for="edit-name">Name:</label>
          <input type="text" id="edit-name" v-model="editedStudent.name" required>
        </div>
        <div>
          <label for="edit-email">Email:</label>
          <input type="email" id="edit-email" v-model="editedStudent.email" required>
        </div>
        <button type="submit">Update</button> <br>
        <button @click="cancelEdit">Cancel</button>
      </form>
    </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      students: Array, // This prop will be passed from the Laravel controller
    },
    // methods: {
    //   editStudent(student) {
    //     // Implement the edit functionality here
    //   },
    //   deleteStudent(studentId) {
    //     // Implement the delete functionality here
    //   },
    // },

    data() {
      return {
        editingStudent: null,
        editedStudent: {
          name: '',
          email: '',
        },
      };
    },
  
    methods: {
      // ... Existing methods ...
      
      editStudent(student) {
        this.editingStudent = student;
        this.editedStudent = { ...student }; // Create a copy of the student for editing
      },
      
      cancelEdit() {
        this.editingStudent = null;
      },
      
      async updateStudent() {
        try {
          const response = await this.$inertia.put(`/students/${this.editingStudent.id}`, this.editedStudent);
          this.editingStudent = null;
          // Optionally, you can show a success message or handle other actions here.
        } catch (error) {
          // Handle error, show validation errors, etc.
        }
      },
    },
 };
</script>
  