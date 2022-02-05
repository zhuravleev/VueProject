<template>
  <div>
    <HeadComp />
    <Nuxt />
    <div class="footer__wrapper">
      <Footer />
    </div>
  </div>
</template>
<script>
import HeadComp from '@/components/HeadComp.vue'
import Footer from '@/components/Footer.vue'
export default {
  name: 'DefaultLayout',
  components: {
    HeadComp,
    Footer,
  },
}
</script>

<style>
.footer__wrapper {
  position: fixed;
  width: 100%;
  bottom: 0;
}
</style>
