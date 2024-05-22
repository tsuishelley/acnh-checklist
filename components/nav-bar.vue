<template>

  <div class="container">
    <div class="user">
    <div class="demographic">
      <div class="chip time">
      Your Time
      </div>
        <div class="current-time">
      {{ currentTime }}
    </div>
    </div>
    <div class="demographic">
          <div class="chip season">
      Your Season
      </div>
        <div class="current-season">
      {{ currentSeason }}
      </div>
      </div>
      <div class=demographic>
      <div class="chip hemisphere">
      Hemisphere
      </div>
          <div class="current-hemisphere">
      {{ currentHemisphere }}
    </div>
    </div>

    </div>
    <div class="sidebar">
      <NuxtLink to="/" class="pill">
        Fish
      </NuxtLink>
            <NuxtLink to="/bug" class="pill">
        Bugs
      </NuxtLink>
            <NuxtLink to="/about" class="pill">
        About
      </NuxtLink>
    </div>
  </div>
</template>


<style>
.container {
  display: flex;
  flex-direction: row;
  align-items: flex-end;
  margin-bottom:50px;
  justify-content:space-between;
}

.user {
  display: flex;
}

.sidebar {
  display: flex;
}

.demographic {
  display: flex;
  flex-direction: column;
}

.chip {
  display: flex;
  justify-content:center;
  padding: 5px 10px; /* Adjust padding as needed */
  margin-left:-20px;
  margin-bottom:-10px;
  max-width:100px;
  color: #725c4e;
  border-radius: 20px;
  font-family: Roboto;
  transform: rotate(-10deg);
  font-size: 14px;
}

.time {
  background-color: #ecdf52;
}

.season {
  background-color: #82d5bb;
}

.hemisphere {
  background-color: #D1DA49;
}

.current-time,
.current-season,
.current-hemisphere {
  padding: 20px 30px;
  border-radius: 40px;
  text-decoration: none;
  background-color: white;
  color: #8a7b66;
  font-size: 18px;
  margin-right:20px;
}

.pill {
  padding: 20px 30px;
  border-radius: 40px;
  text-decoration: none;
  background-color: #725c4e;
  margin-left: 20px;
  color: white;
}

.pill:hover {
  background-color: #8a7b66;
  color: white;
      animation: wiggle 1s; /* Apply the animation */

}

@media (max-width: 1200px) {
  .current-time, .current-season, .current-hemisphere, .chip {
    display:none;
  }
  .container {
    margin-bottom:20px;
      --bs-gutter-x:0px;
  }


}

@media (max-width: 768px){
  a {
    font-size:16px !important;
  }
}

.header {
  font-family: Roboto;
}
@keyframes wiggle {
  0%, 7% {
    transform: rotateZ(0);
  }
  15% {
    transform: rotateZ(-15deg);
  }
  20% {
    transform: rotateZ(10deg);
  }
  25% {
    transform: rotateZ(-10deg);
  }
  30% {
    transform: rotateZ(6deg);
  }
  35% {
    transform: rotateZ(-4deg);
  }
  40%, 100% {
    transform: rotateZ(0);
  }
}



</style>


<script>
export default {
  
  name: 'NavBar',
  data() {
    return {
      currentTime: '',
      currentSeason: '',
      currentHemisphere: ''
    };
  },
  mounted() {
    this.updateTimeAndSeason();
  },
  methods: {
    updateTimeAndSeason() {
      const now = new Date();
      let hour = now.getHours();
  const minute = now.getMinutes();
  const period = hour >= 12 ? 'PM' : 'AM';
  
  // Convert to 12-hour format
  hour = hour % 12 || 12;

  this.currentTime = `${hour}:${minute < 10 ? '0' + minute : minute} ${period}`;
      this.currentSeason = this.getSeason(now.getMonth());
      this.currentHemisphere = this.getHemisphere(now.getMonth());
    },
    getSeason(month) {
      switch (month) {
        case 11: // December, January, February
        case 0:
        case 1:
          return 'Winter';
        case 2: // March, April, May
        case 3:
        case 4:
          return 'Spring';
        case 5: // June, July, August
        case 6:
        case 7:
          return 'Summer';
        default: // September, October, November
          return 'Fall';
      }
    },
    getHemisphere(month) {
      return month >= 2 && month <= 7 ? 'Northern' : 'Southern';
    }
  }
};
</script>