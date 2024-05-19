<template>
  <div class="app">
    <div class="about-row">
      <div class="col">
        <h1>About Me</h1>
        <p>This site was created as a final project for the UW Certificate in Front-End Development by myself, Shelley Tsui. Thank you so much to my instructor Aaron for all the kind help, September Works for providing me with the opportunity to learn front-end development, and most importantly my husband Christian for supplying me with endless mugs of tea and snacks throughout all three courses.</p>
      </div>
      <div class="col" style="position: relative;">
        <img src="/assets/acnh-shelley.svg" class="me" alt="" style="position: absolute; right: 10%;">
      </div>
    </div>
    <h2>
    Resources
    </h2>
    <p>Animal Crossing Character Maker by ______</p>
    <p>Animal Crossing UI Kit by <a href="https://manaloka.com">Kat Manalo</a></p>
    <p>Animal Crossing Data from <a href="https://api.nookipedia.com/">Nookipedia API</a></p>
  </div>
</template>

<style>
.about-row {
  display: flex;
}

a {
    font-family: "Roboto", sans-serif;
  line-height: 150%;
  font-size:18px;
    color: #725C4E;
}

.col {
  flex: 1;
}

img.me {
  max-width: 100%;
  height: auto;
}
</style>