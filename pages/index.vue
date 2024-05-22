<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Fish Checklist</h1>
      <p>All the fish available to catch in Animal Crossing New Horizons along with their location, sell value, and availability. It also includes a checkbox for you to mark what you have and haven't caught. Feel free to use as you see fit!</p>
    </main>
    <div
  class="row"
  v-for="(fish, index) in fishes"
  :key="fish.id + '-' + index"
  :class="{ 'checked-row': fish.checked }"
>
      <img class="col" :src="fish.image_url" alt="Fish Image">
      <h2 class="col">{{ fish.name }}</h2>
      <h2 class="col">{{ fish.location }}</h2>
<h2 class="col">
  <img src="/assets/bells.svg" alt="Bells Icon" class="bell-icon" style="width:20px">
  &nbsp;
    {{ fish.sell_nook }}
</h2>
      <h2 class="col">{{ hemisphere === 'northern' ? fish.north.months : fish.south.months }}</h2>
      <div class="col checkbox-container">
        <input
          class="form-check-input"
          type="checkbox"
          :id="'checkbox-' + fish.id"
          v-model="fish.checked"
          aria-label="..."
        />
        <label :for="'checkbox-' + fish.id" class="custom-checkbox"></label>
      </div>
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
  background-color:#F5EEE1;
  background-image: url('/assets/background-image.jpg');
  background-size: 100%;
  margin: 40px 15% 10% 15%;
  background-attachment: fixed;
  background-repeat:no-repeat;
  background-position: center bottom;
}

main {
  margin-bottom: 50px;
}

@media (max-width: 1200px) {
  h1 {
    font-size: 32px;
  }

  html {
    margin: 20px 10% 5% 10% !important;
  }

    .col:nth-child(4) {
    display: none;
  }
    .main {
    margin-bottom:30px !important;
  }

}

@media (max-width: 768px){
  .app {
    padding:30px !important;
  }

  p {
    font-size:16px !important;
  }

  h2 {
    font-size:16px !important;
  }

  .main {
    margin-bottom:30px !important;
  }
}


.checked-row {
  background-color: #C7ECE0; /* Color when checkbox is checked */
}

.checked-row img {
    animation: wiggle 1s; /* Apply the animation */

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
  name: 'HomePage',

  head() {
    return {
      title: 'Fish Page - Animal Crossing: New Horizons',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'A quick checklist for all the fish you can catch in Animal Crossing New Horizons.'
        }
      ]
    };
  },

  setup() {
    const fishes = ref([]);
    const hemisphere = ref(getHemisphere()); // Set hemisphere based on user's timezone

async function fetchData() {
    try {
        const response = await fetch('https://api.nookipedia.com/nh/fish', {
            headers: {
                'x-api-key': 'ab94348a-c764-4856-b1c1-103cfe6ae2ff'
            }
        });
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        const data = await response.json();
        console.log(data);  // Log the data to inspect its structure
        
        const ids = new Set(); // Create a set to store unique ids
        
fishes.value = data.map((fish, index) => {
    const id = ids.has(fish.id) ? fish.id + '-' + index : fish.id;
    ids.add(id); // Add id to set
    return {
        ...fish,
        id, // Use the modified id
        northAvailability: fish.north.availability_array,
        southAvailability: fish.south.availability_array,
        checked: false // Initialize checked property for each fish
    };
});
    } catch (error) {
        console.error('Error fetching fish data:', error);
    }
}

    function getHemisphere() {
      const now = new Date();
      const month = now.getMonth() + 1; // JavaScript months are zero-based
      return month >= 6 && month <= 11 ? 'southern' : 'northern';
    }

    async function toggleCheckbox(fish) {
      fish.checked = !fish.checked; // Toggle the checked property
    }

    onMounted(fetchData);

    return {
      fishes,
      hemisphere,
      toggleCheckbox
    };
  }
};
</script>