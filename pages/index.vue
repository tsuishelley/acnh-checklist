<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Fish Checklist</h1>
      <p>This checklist shows all the fish available to catch in Animal Crossing New Horizons along with their location, shadow, and rarity. Feel free to use this resource as you see fit!</p>
    </main>
    <div class="heading-row">
       <h2 class= "col">Name</h2>
        <h2 class= "col">Location</h2>
        <h2 class= "col">Shadow</h2>
        <h2 class= "col">Rarity</h2>
        <h2 class= "col">Caught</h2>
    </div>
    <div class="row" v-for="fish in fishes" :key="fish.id">
    <img class="col" :src="fish.image_url" alt="Fish Image">
      <h2 class="col">{{ fish.name }}</h2>
      <h2 class="col">{{fish.location}}</h2>
      <h2 class="col">{{fish.shadow_size}}</h2>
      <h2 class="col">{{fish.rarity}}</h2>
      <input class="form-check-input" type="checkbox" id="checkboxNoLabel" value="" aria-label="...">
    </div>
  </div>
</template>

<style>
img.col {
  max-width: 75px; /* Adjust the width as needed */
}

h2.col {
  margin:0px;
}

.app {
  background-color: white;
  padding: 5% 5% 5% 5%;
}

.heading-row {
  display: flex;
  background-color: #8A7B66;
  border-radius: 10px;
  align-items: center;
  padding: 10px 20px 10px 20px;
  margin-bottom:5px;
  width:100%;
}

.heading-row h2 {
  color:white;
  margin: 0px;
  font-weight: 400;
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
  display: flex;
  align-items: center;
  justify-content: space-between; /* Adjust as needed */
  background-color: #F8F4E8;
  border-radius: 10px;
  width: 100%;
  padding-right: 20px;
  margin: 0 2px 5px 0; /* Add padding to match the heading row */
}

html {
  background-image: url('/assets/background-image.jpg');
  background-size: 100%;
  height:100%;
  margin: 5% 15% 10% 15%;
  background-attachment: fixed;
}


main {
  margin-bottom: 50px;
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