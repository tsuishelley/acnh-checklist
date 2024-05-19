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
      try {
        const response = await fetch('https://api.nookipedia.com/nh/fish', {
          headers: {
            // Add your access key here
            'x-api-key': 'ab94348a-c764-4856-b1c1-103cfe6ae2ff'
          }
        });
        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        console.log(data);  // Log the data to inspect its structure
        fishes.value = data;
      } catch (error) {
        console.error('Error fetching fish data:', error);
      }
    };

    onMounted(fetchData);

    return {
      fishes
    };
  }
};
</script>