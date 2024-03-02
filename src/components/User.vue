  <template>
    <div class="q-pa-md" style="max-width: 350px">
      <q-list dense bordered padding class="item-section rounded-borders">
        <q-item clickable v-ripple class="">
          <q-item-section>
            {{ user.id }}
          </q-item-section>
        </q-item>

        <q-item clickable v-ripple>
          <q-item-section>
           Name: {{ user.name }}
          </q-item-section>
        </q-item>

        <q-item clickable v-ripple>
          <q-item-section>
            Email: {{ user.email }}
          </q-item-section>
        </q-item>
      </q-list>
    </div>
  </template>

  <script setup>
  import { defineProps } from 'vue';

  const props = defineProps({
    user: Object
  });
  </script>

  <style>
  .item {
    color: red;
  }

  .item-section {
    border-color: blue;
    border-style: double;
  }
  </style>

