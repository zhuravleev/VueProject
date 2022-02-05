<template>
  <div>
    <div v-if="info && deliviries">
      <h1 class="heading">Главная страница</h1>
      <img class="mainimage" :src="info.image" alt="" />
      <p v-html="info.text" class="main__text"></p>
      <h2>Доставки</h2>
      <div class="delivery__container">
        <div v-for="(el, i) in del" :key="i" class="delivery">
          <div v-if="el.type === 'train'" class="train">
            <p>Type of delivery: {{ el.type }}</p>
            <p>Departure city: {{ el.departure_city }}</p>
            <p>Departure address: {{ el.departure_address }}</p>
            <p>Destination city: {{ el.destination_city }}</p>
            <p>Destination address: {{ el.destination_address }}</p>
            <p>Weight: {{ el.weight }}</p>
            <p>Volume: {{ el.volume }}</p>
            <img src="train_img.jpg" class="image" alt="" />
          </div>
          <div v-else-if="el.type === 'plane'" class="plane">
            <p>Type of delivery: {{ el.type }}</p>
            <p>Departure city: {{ el.departure_city }}</p>
            <p>Departure address: {{ el.departure_address }}</p>
            <p>Destination city: {{ el.destination_city }}</p>
            <p>Destination address: {{ el.destination_address }}</p>
            <p>Weight: {{ el.weight }}</p>
            <p>Volume: {{ el.volume }}</p>
            <img src="plane_img.jpg" class="image" alt="" />
          </div>
          <div v-else-if="el.type === 'truck'" class="truck">
            <p>Type of delivery: {{ el.type }}</p>
            <p>Departure city: {{ el.departure_city }}</p>
            <p>Departure address: {{ el.departure_address }}</p>
            <p>Destination city: {{ el.destination_city }}</p>
            <p>Destination address: {{ el.destination_address }}</p>
            <p>Weight: {{ el.weight }}</p>
            <p>Volume: {{ el.volume }}</p>
            <img src="truck_img.jpg" class="image" alt="" />
          </div>
          <div v-else class="ship">
            <p>Type of delivery: {{ el.type }}</p>
            <p>Departure city: {{ el.departure_city }}</p>
            <p>Departure address: {{ el.departure_address }}</p>
            <p>Destination city: {{ el.destination_city }}</p>
            <p>Destination address: {{ el.destination_address }}</p>
            <p>Weight: {{ el.weight }}</p>
            <p>Volume: {{ el.volume }}</p>
            <img src="ship_img.jpg" class="image" alt="" />
          </div>
        </div>
      </div>
    </div>
    <LoaderComp v-else />
  </div>
</template>

<script>
import { mapGetters } from 'vuex'
import LoaderComp from '@/components/LoaderComp.vue'
export default {
  name: 'IndexPage',
  components: { LoaderComp },
  layout: 'DefaultLayout',
  data() {
    return {
      info: null,
      del: null,
    }
  },
  computed: {
    ...mapGetters({
      infoData: 'mainpage/getMainPage',
      deliviries: 'mainpage/getDel',
    }),
  },
  async mounted() {
    const data = await this.infoData
    this.info = data.data

    const dataa = await this.deliviries
    this.del = dataa.data
  },
}
</script>

<style>

.mainimage {
  display: block;
  max-width: 600px;
  margin: 0 auto;
  border-radius: 20px;
}
.main__text {
  padding: 20px;
}
.delivery {
  margin: 10px auto;
  text-align: center;
  border: solid;
  padding: 10px;
}

.delivery__container{
  display: flex;
  flex-direction: row; 
  flex-wrap: wrap;
}

.ship{
  display: flex;
  flex-direction: column;
  color: red; 
}
.truck{
  color: rgb(99, 31, 209); 
}
.plane{
  color: rgb(75, 255, 246); 
}
.train{
  color: rgb(236, 255, 62); 
}
.image{
  width: 25px;
  height: 25px;
}
</style>
