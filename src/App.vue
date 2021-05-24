<template>
  <div class="center">
    <router-view />
  </div>
</template>

<style lang="scss">
@import url("https://use.typekit.net/eqp3quc.css");

html,
body {
  background-color: #0c0c0c;
  padding: 0;
  margin: 0;
  overflow: hidden;
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  font-family: sofia-pro;

  @media not all and (hover: hover) {
    height: 100%;
  }
}
</style>
