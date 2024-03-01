<template>
    <div class="q-pa-md" style="max-width: 350px">
    <q-list dense bordered padding class="rounded-borders">
      <q-item clickable v-ripple>
        <q-item-section>
          {{ user.id }}
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple>
        <q-item-section>
          {{ user.name }}
        </q-item-section>
      </q-item>

      <q-item clickable v-ripple>
        <q-item-section>
          {{ user.email }}
        </q-item-section>
      </q-item>
    </q-list>
  <div v-if="error" class="error">Error: {{ error }}</div>
  </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import axios from 'axios';

  const user = ref([{}]);
  const isLoading=ref(false);
  const props = defineProps({
  userId: Number,
  userIndex: Number
});
  
  const fetchUser = async () => {
    try {
      isLoading.value = true;
      const response = await axios.get(`https://jsonplaceholder.typicode.com/users/${props.userId}`);
      user.value = response.data;
      isLoading.value = false;
    } catch (error) {
      isLoading.value = false;
      console.error('Error fetching post:', error);
    }
  }
  
 
  fetchUser(props.userId); // Fetch user data when component is mounted, using the provided userId
   
  </script>
  