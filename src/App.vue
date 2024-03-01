<template>
  <div>
    <q-banner :class="$q.dark.isActive ? 'bg-grey-9' : 'bg-grey-3'">
      <template v-slot:avatar>
        <q-icon name="people" color="primary" />
      </template>
      Fetching User Data from a REST API
      <template v-slot:action>
        <q-btn color="primary" :loading="isLoading" label="Fetch Users" @click="fetchUsers"></q-btn>
      </template>
    </q-banner>
    <h1>User Data</h1>
    
    <ul v-if="users">
      <span v-for="(user,index) in users" :key="user.id">
        <User :user="user" :userId="user.id" :userIndex="index"/>
      </span>
    </ul>
  </div>

</template>

<script setup>

import { ref } from 'vue';
import axios from 'axios';
import User from './components/User.vue';

const users = ref([]);
const isLoading=ref(false);

const fetchUsers = async () => {
  try {
    isLoading.value = true;
    const response = await axios.get('https://jsonplaceholder.typicode.com/users');
    users.value = response.data;
    isLoading.value = false;
  } catch (error) {
    isLoading.value = false;
    console.error('Error fetching posts:', error);
  }
}
</script>
