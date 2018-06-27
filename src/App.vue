<template>
  <div id="app">
    <div class="cover"></div>
    <Header />
    <Todos />
    <Footer />
  </div>
</template>

<script>
import Footer from './components/Footer.vue'
import Header from './components/Header.vue'
import Todos from './components/Todos.vue'
export default {
  name: 'App',
  components : {
    Header,
    Todos,
    Footer,   
  }
}
</script>

<style lang = "less" scoped>
    #app {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0
    }

    .cover {
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        background-color: #555;
        opacity: 0.5;
        z-index: -1
    }
</style>
