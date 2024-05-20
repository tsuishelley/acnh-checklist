<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Bugs Checklist</h1>
      <p>All the bugs available to catch in Animal Crossing New Horizons along with their location, sell value, and availability. It also includes a checkbox for you to mark what you have and haven't caught. Feel free to use as you see fit!</p>
    </main>
    <div
      class="row"
      v-for="bug in bugs"
      :key="bug.id"
      :class="{ 'checked-row': bug.checked }"
    >
      <img class="col" :src="bug.image_url" alt="Bug Image">
<h2 class="col">{{bug.name }}</h2>
      <h2 class="col">{{ bug.location }}</h2>
<h2 class="col">

  <img src="/assets/bells.svg" alt="Bells Icon" class="bell-icon" style="width:20px">
  &nbsp;
    {{ bug.sell_nook }}
</h2>
      <h2 class="col">{{ hemisphere === 'northern' ? bug.north.months : bug.south.months }}</h2>
      <div class="col checkbox-container">
        <input
          class="form-check-input"
          type="checkbox"
          :id="'checkbox-' + bug.id"
          v-model="bug.checked"
          aria-label="..."
        />
        <label :for="'checkbox-' + bug.id" class="custom-checkbox"></label>
      </div>
    </div>
  </div>
</template>


<style>
img.col {
  max-width: 75px; /* Adjust the width as needed */
}

h2.col {
  margin: 0;
}

.app {
  background-color: white;
  padding: 5%;
  border-radius: 40px !important;
}

p {
  color: #725C4E;
  opacity: 0.75;
  padding-top: 10px;
}

h1 {
  font-weight: 700;
  color: #725C4E;
}

h2 {
  font-family: "Roboto", sans-serif;
  font-weight: 400;
  line-height: 150%;
  font-size: 16px;
  color: #725C4E;
}

.row {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: #F8F4E8;
  border-radius: 10px;
  width: 100%;
  padding-right: 20px;
  margin: 0 2px 5px 0;
  transition: background-color 0.3s ease;
}

.checked-row {
  background-color: #C7ECE0; /* Color when checkbox is checked */
}

html {
  background-image: url('/assets/background-image.jpg');
  background-size: 100%;
  margin: 40px 15% 10% 15%;
  background-attachment: fixed;
}

main {
  margin-bottom: 50px;
}

.checkbox-container {
  display: flex;
  justify-content: flex-end;
  max-width: 50px;
  position: relative;
}

.form-check-input {
  display: none; /* Hide the default checkbox */
}

.custom-checkbox {
  width: 30px;
  height: 30px;
  cursor: pointer;
  background: url('/assets/unchecked.svg') no-repeat center center / contain;
}

.form-check-input:checked + .custom-checkbox {
  background: url('/assets/checked.svg') no-repeat center center / contain;
}

</style>

<script>
import { ref, onMounted } from 'vue';

export default {
  name: 'BugPage',
  setup() {
    const bugs = ref([]);
    const hemisphere = ref(getHemisphere()); // Set hemisphere based on user's timezone

async function fetchData() {
  try {
    const response = await fetch('https://api.nookipedia.com/nh/bugs', {
      headers: {
        'x-api-key': 'ab94348a-c764-4856-b1c1-103cfe6ae2ff'
      }
    });
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    console.log(data);  // Log the data to inspect its structure
    bugs.value = data.map(bug => ({
      ...bug,
      name: capitalizeFirstLetter(bug.name), // Capitalize the first letter of bug name
      northAvailability: bug.north.availability_array,
      southAvailability: bug.south.availability_array,
      checked: false  // Ensure each bug has its own 'checked' property
    }));
  } catch (error) {
    console.error('Error fetching bug data:', error);
  }
}

    function getHemisphere() {
      const now = new Date();
      const month = now.getMonth() + 1; // JavaScript months are zero-based
      return month >= 6 && month <= 11 ? 'southern' : 'northern';
    }

     function capitalizeFirstLetter(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }

    onMounted(fetchData);

    return {
      bugs,
      hemisphere
    };
  }
};
</script>