<template>
    <div>
      <h1>Student List</h1>
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
    </div>
  </template>
  
  <script>
  export default {
    props: {
      students: Array, // This prop will be passed from the Laravel controller
    },
    methods: {
      editStudent(student) {
        // Implement the edit functionality here
      },
      deleteStudent(studentId) {
        // Implement the delete functionality here
      },
    },
  };
  </script>
  