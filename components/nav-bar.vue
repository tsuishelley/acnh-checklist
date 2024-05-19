
<template>
<div
class="header">
      <div
class="sidebar">
        <NuxtLink
to="/">
          Home
        </NuxtLink>
        <NuxtLink
to="/about">
          About
        </NuxtLink>

    </div>

 </div>

 </template>


<style>
body {
  background-color:white;
}
.header {
display:flex;
flex-direction:row;
}
</style>

 <script>
export default {
  name: 'NavBar',
}
 </script>