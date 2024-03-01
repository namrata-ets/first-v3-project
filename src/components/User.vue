<template>
    <div class="user">
      <h3>{{ user.id }}</h3>
      <p>{{ user.name }}</p>
      <p>{{ user.email }}</p>
      <div v-if="error" class="error">Error: {{ error }}</div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';

  const user = ref([{}]);
  const props = defineProps({
  userId: String,
  userIndex: Number
});
  
  const fetchUser = async () => {
    try {
      const response = await axios.get(`https://jsonplaceholder.typicode.com/users/${props.userId}`);
      user.value = response.data;
    } catch (error) {
      console.error('Error fetching post:', error);
    }
  }
  
 
  fetchUser(props.userId); // Fetch user data when component is mounted, using the provided userId
   
  </script>
  