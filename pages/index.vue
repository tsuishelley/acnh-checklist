<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Fish List</h1>
      <p>This checklist allows you to see what fish you’re currently able to catch in Animal Crossing depending on your time, season, and location. Feel free to use this resource as you see fit!</p>
      <div class="row">
        <div v-for="fish in fishList" :key="fish.id">
          <p>{{ fish.name }}</p>
        </div>
      </div>
    </main>
  </div>
</template>

<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api';
import axios from '@nuxtjs/axios';

export default defineComponent({
  data() {
    return {
      fishList: []
    };
  },
  async mounted() {
    try {
      const response = await axios.get('/villagers');
      this.fishList = response.data;
    } catch (error) {
      console.error('Error fetching fish data:', error);
    }
  },
});
</script>


<style>
p {
  font-family: sans-serif;
  color: #725C4E;
  opacity: .75;
  padding-top: 10px;
}

h1 {
  font-family: sans-serif;
  font-weight: 700;
  color: #725C4E;
}

html {
    background-color: #EEE9CA;
    margin: 5% 15% 10% 15%;
}

body {
    background-color:white;
}

</style>