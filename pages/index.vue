<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Fish List</h1>
      <p>This checklist allows you to see what fish you’re currently able to catch in Animal Crossing depending on your time, season, and location. Feel free to use this resource as you see fit!</p>
    </main>
    <div v-for="fish in fishes" :key="fish.id">
      <h1>{{ fish.name }}</h1>
    </div>
  </div>
</template>

<style>
.app {
  margin: 5% 15% 10% 15%;
  background-color: white;
}

p {
  color: #725C4E;
  opacity: .75;
  padding-top: 10px;
}

h1 {
  font-weight: 700;
  color: #725C4E;
}

html {
  background-color: #EEE9CA;
}
</style>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'HomePage',
  setup() {
    const fishes = ref([]);

    const fetchData = async () => {
      const response = await fetch('https://api.nookipedia.com/nh/fish');
      const data = await response.json();
      fishes.value = data;
    };

    onMounted(fetchData);

    return {
      fishes
    };
  }
};
</script>