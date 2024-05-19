<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Fish List</h1>
      <p>This checklist allows you to see what fish you’re currently able to catch in Animal Crossing depending on your time, season, and location. Feel free to use this resource as you see fit!</p>
    </main>
    <div class="row" v-for="fish in fishes" :key="fish.id">
    <img class="col" :src="fish.image_url" alt="Fish Image" style="max-height: 50px;">
      <h2 class="col">{{ fish.name }}</h2>
      <h2 class="col">{{fish.location}}</h2>
      <h2 class="col">{{fish.shadow_size}}</h2>
    </div>
  </div>
</template>

<style>
.app {
  background-color: white;
  padding: 5% 5% 5% 5%;
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

h2 {
  font-family: "Roboto", sans-serif;
  font-weight: 700;
  line-height: 150%;
  font-size: 16px;
    color: #725C4E;
}

.row {
  display:flex;
  background-color: #F8F4E8;
  margin-bottom: 5px;
  border-radius: 20px;
  padding: 5px;
}

html {
  background-color: #EEE9CA;
  margin: 5% 15% 10% 15%;
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