<template>
  <div class ="app">
    <body>
      <main class="main">
          <h1>Animal Crossing Fish List</h1>
        <p>This checklist allows you to see what fish you’re currently able to catch in Animal Crossing depending on your time, season, and location. Feel free to use this resource as you see fit!</p>
      </main>
    </body>
  </div>
</template>

<style>
p {
  color: #725C4E;
  opacity: .75;
  padding-top: 10px;
}
h1 {
  font-weight: 700;
  color: #725C4E;
}
html {
    background-color: #EEE9CA;
    margin: 5% 15% 10% 15%;
}
body {
    background-color:white;
}
</style>

<script>
definePageMeta ({
  layout: 'test'
})

//Fetch all fish
const {data:test} = await useFetch('https://api.nookipedia.com/nh/fish');
export default {
  name: 'HomePage',
}
</script>