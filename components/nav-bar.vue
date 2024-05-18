<template>
<div class="header">
      <div class="user-info">
      <div class="time">
        <div class = "time-label">
          Time
        </div>
      </div>
      <div class="date">
        <div class = "date-label">
          Date
        </div>
      </div>
      <div class="hemisphere">
        <div class = "hemisphere-label">
          Hemisphere
        </div>
      </div>
    </div>
      <div class="sidebar">
        <div class="checklist">Checklist</div>
        <div class="about">About</div>
    </div>
 </div>
 </template>

<style>

body {
  border-radius: 30px;
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