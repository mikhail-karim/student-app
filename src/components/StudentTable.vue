<template>
    <div class="table-container">
        <h1>Daftar Mahasiswa</h1>
        <table border="1">
        <thead>
            <tr>
            <th>ID</th>
            <th>NPM</th>
            <th>Nama</th>
            <th>Angkatan</th>
            <th>IPK</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="mhs in mahasiswa" :key="mhs.id">
            <td>{{ mhs.id }}</td>
            <td>{{ mhs.npm }}</td>
            <td>{{ mhs.nama }}</td>
            <td>{{ mhs.angkatan }}</td>
            <td>{{ mhs.ipk }}</td>
            </tr>
        </tbody>
        </table>
    </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'StudentTable',
  data() {
    return {
      mahasiswa: []
    };
  },
  mounted() {
    axios.get('https://api-lumen-with-jwt-production.up.railway.app/student')
      .then(res => {
        console.log('Data mahasiswa dari API:', res.data.data);
        this.mahasiswa = res.data.data; // pastikan ini cocok
      })
      .catch(err => {
        console.error('Gagal ambil data mahasiswa:', err);
      });
  }
};
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

.table-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  font-family: 'Inter', sans-serif;
  background-color: #f9f9f9;
  min-height: 100vh;
  padding-top: 40px;
}

h1 {
  color: #2c3e50;
  margin-bottom: 20px;
}

table {
  border-collapse: collapse;
  width: 90%;
  max-width: 800px;
  background-color: #ffffff;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  overflow: hidden;
}

th, td {
  padding: 12px 20px;
  text-align: left;
}

thead {
  background-color: #2c3e50;
  color: #ffffff;
}

tbody tr:nth-child(even) {
  background-color: #f0f0f0;
}

tbody tr:hover {
  background-color: #e0f7fa;
  transition: background-color 0.3s;
}
</style>
