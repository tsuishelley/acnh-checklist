<template>
  <div class="app">
    <div class="about-row">
      <div class="col-7">
        <h1>About</h1>
        <p>This site was created as a final project for the UW Certificate in Front-End Development by myself, Shelley Tsui. Thank you so much to my instructor Aaron for all the kind help, September Works for providing me with the opportunity to learn front-end development, and most importantly my husband Christian for supplying me with endless mugs of tea and snacks throughout all three courses.</p>
      <br>
      <p>As for my own Animal Crossing preferences — I'm a big fan of Fauna, Sally, and Kapp'n's lovely sea shanties. My passport title is Untossable Trash. If you're interested in seeing more of my work, click here. </p>
      </div>
      <div class="col" style="position: relative;">
        <img src="/assets/acnh-shelley.svg" class="me" alt="" style="position: relative; right: 10%;">
      </div>
    </div>
    <hr>
    <h3>
    Resources
    </h3>
    <p>Animal Crossing Character Maker by <a href="https://www.figma.com/@ace">Ace S Chen</a></p>
    <p>Animal Crossing UI Kit by <a href="https://manaloka.com">Kat Manalo</a></p>
    <p>Animal Crossing Data from <a href="https://api.nookipedia.com/">Nookipedia API</a></p>
  </div>
</template>

<style>
.about-row {
  display: flex;
      flex-wrap:wrap;
    align-content: center;
}

a {
    font-family: "Roboto", sans-serif;
  line-height: 150%;
  font-size:18px;
    color: #725C4E;
}

h3 {
    font-size:32px;
    font-family:Poppins;
    font-weight:700;
  color: #725C4E;
  margin-top:50px;
}

.col-7{
  flex: 2;
  margin-right:80px;
  margin-bottom:100px;
}

img.me {
  max-width: 100%;
  border-radius: 30px;
}
</style>