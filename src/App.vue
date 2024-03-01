<template>
  <div>
    <h1>Users</h1>
    <button @click="fetchPosts">Fetch Users</button>
    <ul v-if="users">
      <li v-for="(user,index) in users" :key="user.id">
        <User :user="user" :userId="user.id" :userIndex="index"/>
      </li>
    </ul>
  </div>
</template>

<script setup>

import { ref } from 'vue';
import axios from 'axios';
import User from './components/User.vue';

const users = ref([]);

const fetchPosts = async () => {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/users');
    users.value = response.data;
  } catch (error) {
    console.error('Error fetching posts:', error);
  }
}
</script>
