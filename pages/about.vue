<template>
  <div>
    <div v-if="info">
      <h1 class="heading">All about us</h1>
      <p class="about__text">{{ info.text }}</p>
    </div>
    <LoaderComp v-else />
  </div>
</template>
<script>
import { mapGetters } from 'vuex'
import LoaderComp from '@/components/LoaderComp.vue'
export default {
  name: 'AboutPage',
  components: { LoaderComp },
  layout: 'DefaultLayout',
  data() {
    return {
      info: null,
    }
  },
  computed: {
    ...mapGetters({
      infoData: 'mainpage/getAboutPage',
    }),
  },
  async mounted() {
    const data = await this.infoData
    this.info = data.data
  },
}
</script>

<style>
.about__text {
  padding: 20px;
}
</style>
