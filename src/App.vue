<template>
  <nav class='app'>
    <router-link to="/">
      <img alt="Vue logo" src="./assets/logo.png">
    </router-link> |
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </nav>
  <router-view/>
</template>

<style lang="scss" scoped>
img {
  width: 30px;
}
</style>
