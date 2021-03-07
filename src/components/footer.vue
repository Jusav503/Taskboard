<template>
  <div id="footerLolweb" class="footerLol">
    <figure>
      <img class="logo" src="https://www.pinclipart.com/picdir/big/156-1563483_free-logo-templates-cat-logo-logo-images-animal.png" alt="cat">
      <h1>LOLWEB</h1>
    </figure>
    <span>
      Justice Ariel Velasco Gómez | 2002-2021
    </span>
  </div>
</template>

<script>

export default {
  name: 'footerLolweb'
}
</script>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Ruluko&display=swap');

.footerLol{
  width: 100%;
  background-color: #000000;
  height: 60px;
  padding: 10px;
  display: flex;
}
figure{
  font-family: 'Ruluko', sans-serif;
  color: #FFFFFF;
  display: flex;
  justify-content: flex-start;
}
.logo{
  width: 40px;
  height: 40px;
}
span{
  font-family: 'Ruluko', sans-serif;
  color: #FFFFFF;
  margin: 0px 300px 0px 300px;
  align-self: center;
}
</style>