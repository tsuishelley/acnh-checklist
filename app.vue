<template>
  <div>
    <NavBar /> <!-- Include the NavBar component -->
    <div class="white-content-box">  <!-- Add the white background and border radius to this div instead of the body -->
     <HomePage /> <!-- Use the component within the template -->
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
.white-content-box {
    margin-top: 20px;
    padding: 60px;
    background-color:white;
}

body {
  background-color:transparent;
}
</style>