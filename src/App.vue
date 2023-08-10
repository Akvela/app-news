<template>
  <Header />
  <main>
    <div class="block">
      <div class="container">
        <h1 class="title">Новости</h1>
      </div>
    </div>
    <Gallery />
    
  </main>
  <Footer />
</template>

<script>
import Header from './components/Header.vue'
import Gallery from './components/Gallery.vue'
import Footer from './components/Footer.vue'

export default {
  components: {
    Header,
    Gallery,
    Footer
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'Nunito Sans', sans-serif;
  }

  .container {
    max-width: 1710px;
    width: 100%;
    margin: 0 auto;
  }

  .block {
    background: url('./images/background.png') center / cover;
    height: 320px;
    padding: 40px;
  }

  .title {
    padding-top: 187px;
    font-size: 40px;
    font-weight: 700;
  }

  @media screen and (max-width: 574px) {
    .title {
      font-size: 26px;
    }
  }
</style>
