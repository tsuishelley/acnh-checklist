<template>

  <div>
  <NavBar />
    <div class="white-content-box">  <!-- Add the white background and border radius to this div instead of the body -->
     <NuxtPage />
    </div>
  </div>
</template>

<script>
// Import the NavBar and HomePage components
import NavBar from './components/nav-bar.vue';
import HomePage from './pages/index.vue';
import BugPage from './pages/bug.vue';
import SeaPage from './pages/sea.vue';
export default {
  name: 'DefaultLayout',
  components: {
    // Register the NavBar and HomePage components
    NavBar,
    HomePage,
    BugPage,
    SeaPage
  }
}
</script>

<style>
@import
url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');

body {
  background-color:transparent !important;
}

h1 {
    font-family: "Poppins", sans-serif;
    font-size: 48px;
}

p {
  font-family: "Roboto", sans-serif;
  line-height: 150%;
  font-size:18px;
}

</style>