<template>
  <Header/>
  <history/>
  <Botview/>
  <Footer/>
</template>

<script>
import history from '@/components/history.vue';
import Header from '@/components/header.vue';
import BotView from '@/components/botview.vue';
import Footer from '@/components/footer.vue';
export default {
    components: {
        history,
        Header,
        BotView,
        Footer,
    }
}
</script>

<style>

</style>