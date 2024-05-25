<template>
  <div class="app">
    <main class="main">
      <h1>Animal Crossing Bugs List</h1>
      <p>All the bugs available to catch in Animal Crossing New Horizons along with the necessary stats. Feel free to use this list to track your progress!</p>
      <div class="progress-container">
        <div class="progress-bar-container">
          <div class="progress-bar" :style="{ width: progressPercentage + '%' }"></div>
        </div>
        <span class="progress-counter">{{ checkedCount }} / {{ bugs.length }}</span>
      </div>
    </main>
    <div
      class="row"
      v-for="(bug, index) in bugs"
      :key="bug.id + '-' + index"
      :class="{ 'checked-row': bug.checked }"
    >
      <img class="col" :src="bug.image_url" alt="Bug Image">
      <h2 class="col">{{ bug.name }}</h2>
      <h2 class="col">{{ bug.location }}</h2>
      <h2 class="col">
        <img src="/assets/bells.svg" alt="Bells Icon" class="bell-icon" style="width:20px">
        &nbsp;{{ bug.sell_nook }}
      </h2>
      <h2 class="col">{{ hemisphere === 'northern' ? bug.north.months : bug.south.months }}</h2>
      <h2 class="col">{{ getBugTimes(bug) }}</h2> <!-- New Column for Times -->
      <div class="col checkbox-container">
        <input
          class="form-check-input"
          type="checkbox"
          :id="'checkbox-' + bug.id"
          v-model="bug.checked"
          @change="saveProgress"
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
  margin:0px;
}

.app {
  background-color: white;
  padding: 5% 5% 5% 5%;
    border-radius: 40px !important;
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
  font-weight: 400;
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
  margin: 0 2px 5px 0; /* Add padding to match the heading row */
}

.progress-container {
  margin-top:40px;
  display: flex;
  align-items: center;
}

.progress-bar-container {
  flex-grow: 1;
  background-color: #F8F4E8;
  border-radius: 10px;
  height: 10px;
  position: relative;
  margin-right: 30px;
    align-items: center;

}

.progress-bar {
  height: 100%;
  background-color: #76c7c0;
  border-radius: 10px;
  transition: width 0.3s ease;
}

.progress-counter {
  color: #725C4E;
  font-weight: 500;
  opacity:75%;
  white-space: nowrap; /* Prevents the text from wrapping */
}

.checked-row {
  background-color: #C7ECE0; /* Color when checkbox is checked */
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

    html {
    margin: 5% 5% 10% 5% !important;
  }

}

@media (max-width:576px) {

    html {
    margin: 5% 3% 10% 3% !important;
  }

      .col:nth-child(3), .col:nth-child(5) {
    display: none;
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
import { ref, onMounted, computed } from 'vue';

export default {
  name: 'HomePage',
  head() {
    return {
      title: 'Bug Page - Animal Crossing: New Horizons',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'A quick checklist for all the bugs you can catch in Animal Crossing New Horizons.'
        }
      ]
    };
  },
  setup() {
    const bugs = ref([]);
    const hemisphere = ref(getHemisphere());

    function getCurrentMonth() {
      const now = new Date();
      return now.getMonth() + 1; // JavaScript months are zero-based, so add 1
    }

    function sortBugsByMonth(bugList, hemisphere, currentMonth) {
      return bugList.sort((a, b) => {
        const aMonths = hemisphere === 'northern' ? a.north.months_array : a.south.months_array;
        const bMonths = hemisphere === 'northern' ? b.north.months_array : b.south.months_array;

        const aAvailable = aMonths.includes(currentMonth);
        const bAvailable = bMonths.includes(currentMonth);

        if (aAvailable && !bAvailable) {
          return -1;
        }
        if (!aAvailable && bAvailable) {
          return 1;
        }
        return 0;
      });
    }

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
        const ids = new Set();
        const currentMonth = getCurrentMonth();
        
        let bugList = data.map((bug, index) => {
          const id = ids.has(bug.id) ? bug.id + '-' + index : bug.id;
          ids.add(id);
          return {
            ...bug,
            id,
            name: capitalizeFirstLetter(bug.name), // Capitalize the first letter of bug name
            northAvailability: bug.north.availability_array,
            southAvailability: bug.south.availability_array,
            checked: false
          };
        });

        // Load saved progress from local storage
        const savedProgress = JSON.parse(localStorage.getItem('bugProgress')) || {};
        bugList.forEach(bug => {
          if (savedProgress[bug.id] !== undefined) {
            bug.checked = savedProgress[bug.id];
          }
        });

        bugList = sortBugsByMonth(bugList, hemisphere.value, currentMonth);
        bugs.value = bugList;
      } catch (error) {
        console.error('Error fetching bug data:', error);
      }
    }

    function getHemisphere() {
      const now = new Date();
      const month = now.getMonth() + 1;
      return month >= 6 && month <= 11 ? 'southern' : 'northern';
    }

    const checkedCount = computed(() => {
      return bugs.value.filter(bug => bug.checked).length;
    });

    const progressPercentage = computed(() => {
      return (checkedCount.value / bugs.value.length) * 100;
    });

    function getBugTimes(bug) {
      const currentMonth = getCurrentMonth();
      const timesByMonth = hemisphere.value === 'northern' ? bug.north.times_by_month : bug.south.times_by_month;
      return timesByMonth[currentMonth];
    }

    function saveProgress() {
      const progress = {};
      bugs.value.forEach(bug => {
        progress[bug.id] = bug.checked;
      });
      localStorage.setItem('bugProgress', JSON.stringify(progress));
    }

    async function toggleCheckbox(bug) {
      bug.checked = !bug.checked;
      saveProgress();
    }

    function capitalizeFirstLetter(str) {
      return str.charAt(0).toUpperCase() + str.slice(1);
    }

    onMounted(fetchData);

    return {
      bugs,
      hemisphere,
      toggleCheckbox,
      checkedCount,
      progressPercentage,
      getBugTimes,
      saveProgress
    };
  }
};
</script>