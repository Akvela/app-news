<template>
  <header class="header">
    <div class="container">
      <img src="../images/logo.png" class="logo">
    </div>
  </header>
</template>

<style scoped>
  .header {
    height: 124px;
    width: 100%;
    padding: 40px;
    box-shadow: 0px 8px 16px 0px #00000014;
  }

  .container {
    max-width: 1710px;
    width: 100%;
    margin: 0 auto;
  }

  @media screen and (max-width: 574px) {
      .logo {
      width: 114px;
      height: 36px;
    }
  }
</style>
