<template>
  <q-container>
    <q-banner :class="$q.dark.isActive ? 'bg-grey-9' : 'bg-grey-3'">
      <template v-slot:avatar>
        <q-icon class="icon-position" name="people" color="primary" />
      </template>
     <span class="title"> Fetching User Data from a REST API </span>
     <template v-slot:action>
        <q-btn class="button-position" color="primary" :loading="isLoading" label="Fetch Data" @click="fetchUsers"></q-btn>
      </template>
    </q-banner>

    <ul v-if="users">
      <span v-for="(user, index) in users" :key="user.id">
        <User :user="user" />
      </span>
    </ul>
  </q-container>
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import User from './components/User.vue';

const users = ref([]);
const isLoading=ref(false);
const error=ref('');
const fetchUsers = async () =>{
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/users');
     //check if the API call is successful status code will be from 200 to 299, else any other status code that indicates API request unsuccessful
      if (!response.status.toString().startsWith('2')) {
          throw new Error(`API error: ${response.status} - ${response.statusText}`);
      }
    users.value = response.data;
  }
  catch (error) {
      isLoading.value = false;
      alert=true;
      console.error('Error fetching users:', error);
        if (error.isAxiosError && error.response) {
              //Check for Network errors or other status code errors
              console.error(`Network error (${error.response.status}): ${error.response.data}`);
            } else {
              // Log any other errors
              console.error('Unexpected error:', error);
            }
  }
  finally {
      isLoading.value = false;
    }
};


</script>
<style>
.title{
  font-family: Georgia, 'Times New Roman', Times, serif;
  font-weight: bold;
  color: black;
  font-size: 50px;
  align-items: center;
  padding-left: 100px;
}
.icon-position{
      padding-top: 50px;
}
.button-position{
    margin-right: 150px;
    margin-top: 50px;
    margin-bottom: 40px;
}
</style>

