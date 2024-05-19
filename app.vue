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
export default {
  name: 'DefaultLayout',
  components: {
    // Register the NavBar and HomePage components
    NavBar,
    HomePage
  }
}
</script>

<style>
@import
url('https://fonts.googleapis.com/css2?family=Poppins:wght@200;300;400;600;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');



.white-content-box {
    margin-top: 20px;
    padding: 60px;
    background-color:white;
}
h1 {
    font-family: "Poppins", sans-serif;
}

p {
  font-family: "Roboto", sans-serif;
  line-height: 150%;
}
</style>