<template>

  <div class="header">
    <div class="user">
    <div class="demographic">
      <div class="chip time">
      Time
      </div>
        <div class="current-time">
      {{ currentTime }}
    </div>
    </div>
    <div class="demographic">
          <div class="chip season">
      Season
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
      <NuxtLink to="/" class="checklist-pill">
        Checklist
      </NuxtLink>
      <NuxtLink to="/about" class="about-pill">
        About
      </NuxtLink>
    </div>
  </div>
</template>

<style>
.demographic {
  display:flex;
  flex-direction:column;
}

.user {
  display:flex;
}

.chip {
    display: inline-block;
    padding: 5px 15px;
    color: #725C4E;
    border-radius: 20px;
    font-family: Roboto;
    transform: rotate(-10deg);
    font-size:14px;
}

.time {
      background-color: #ECDF52;
}

.season {
      background-color: #F7CD67;
}

.hemisphere {
      background-color: #82D5BB;
}

.current-time, .current-season, .current-hemisphere {
  padding: 20px 30px;
  border-radius: 40px;
  text-decoration: none;
  background-color: white;
  color: #8a7b66;
  font-size: 18px;
}

.checklist-pill {
  padding: 20px 30px;
  border-radius: 40px;
  text-decoration: none;
  background-color: #8a7b66;
  margin-right: 20px;
  color: white;
}

.about-pill {
  padding: 20px 30px;
  border-radius: 40px;
  text-decoration: none;
  background-color: white;
  color: #8a7b66;
}

.about-pill:hover {
      animation: wiggle 1.5s linear infinite;
}

.header {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
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
      this.currentTime = now.toLocaleTimeString();
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
          return 'Autumn';
      }
    },
    getHemisphere(month) {
      return month >= 2 && month <= 7 ? 'Northern' : 'Southern';
    }
  }
};
</script>