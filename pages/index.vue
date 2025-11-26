<template>
  <Header/>
  <!-- Outer wrapper with max width and horizontal margin -->
  <div class="max-w-7xl mx-auto px-4">
    
    <Home/>
    <BotView/>
    
  </div>
  <Footer/>
</template>

<script>
import Header from '@/components/header.vue';
import BotView from '@/components/botview.vue';
import Home from '@/components/home.vue';
import Footer from '@/components/footer.vue';

export default {
  components: {
    Header,
    BotView,
    Home,
    Footer,
  }
}
</script>

<style>
/* Optional: you can set min height for full viewport */
body, html {
  margin: 0;
  padding: 0;
}
</style>
