<template>
    <div>
      <h1>Welcome to Home</h1>
      <button @click="logout">Logout</button>
    </div>
  </template>
  
  <script>
  import Swal from 'sweetalert2';
  export default {
    name: 'Logout',
    methods: {
      logout() {
        // ลบ token หรือข้อมูลผู้ใช้จาก localStorage
        localStorage.removeItem('userToken');
        localStorage.removeItem('username');
        localStorage.removeItem('role');
        localStorage.removeItem('_id');
        // นำผู้ใช้ไปยังหน้า Login
        // this.$router.push({ name: 'Login' });
        
      },
    },
  };
  </script>