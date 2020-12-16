<template>
  <header>
    <b-container class="mainheader">
      <div>
        <img src="../../assets/img/coffee1.png" />
        Coffee Shop
      </div>
      <div class="header-menu">
        <router-link to="#">Home</router-link>
        <router-link to="#">Product</router-link>
        <router-link to="#">Your Cart</router-link>
        <router-link to="#">History</router-link>
      </div>
      <div class="header-icon">
        <router-link to="#"
          ><img src="../../assets/img/Vector.png"
        /></router-link>
        <router-link to="#"><img src="../../assets/img/chat.png"/></router-link>
        <router-link to="#"><img src="../../assets/img/prof.png"/></router-link>
      </div>
    </b-container>
  </header>
</template>

<style scoped>
.mainheader {
  display: flex;
  justify-content: space-evenly;
}
</style>
