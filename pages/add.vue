<template>
  <div>
    <form
      v-if="info"
      action="https://demo-api.vsdev.space/api/delivery/sales"
      method="post"
      class="add"
      @submit="send"

    >
      <h1 class="heading">Добавление</h1>
      <label v-for="(item, i) in info" :key="i">
        {{ item.title }}
        <input
          v-if="item.type !== 'select'"
          :id="keys[i]"
          v-model="keys[i]"
          :type="item.type"
          :name="keys[i]"
        />
        <select v-else :name="keys[i]">
          <option
            v-for="value in item.values"
            :id="keys[i]"
            :key="value"
            :value="value"
          >
            {{ value }}
          </option>
        </select>
      </label>
      <button class="button" type="submit" @click="update">Добавить</button>
    </form>
    <LoaderComp v-else />
  </div>
</template>
<script>
import axios from 'axios'
import { mapGetters } from 'vuex'
import LoaderComp from '@/components/LoaderComp.vue'
// import HeadComp from '@/components/HeadComp.vue'
export default {
  name: 'AddPage',
  components: { LoaderComp },
  layout: 'DefaultLayout',
  data() {
    return {
      info: null,
      keys: null,
      type: null,
      departure_city: null,
      departure_address: null,
      destination_city: null,
      destination_address: null,
      weight: null,
      volume: null,
    }
  },
  computed: {
    ...mapGetters({
      infoData: 'mainpage/getForm',
    }),
  },
  async mounted() {
    const data = await this.infoData
    this.info = data.data.fields
    this.keys = Object.keys(data.data.fields)
    console.log(this.keys)
  },
  methods: {
    // update(){
    //   HeadComp.$mount();
    // },

    async send(e) {
      e.preventDefault()
      const data = {}
      if (e.target[0].value && e.target[1].value && e.target[2].value && e.target[3].value && e.target[4].value && e.target[5].value && e.target[6].value){
        data.type = e.target[0].value
        data.departure_city = e.target[1].value
        data.departure_address = e.target[2].value
        data.destination_city = e.target[3].value
        data.destination_address = e.target[4].value
        data.weight = e.target[5].value
        data.volume = e.target[6].value
        console.log(data)
        await axios.post(
          'https://demo-api.vsdev.space/api/delivery/sales',
          data
        )
        e.target.reset();
      }
      else{
        console.log('Заполните форму')
      }
    },
  },
}
</script>
<style>
.about__text {
  padding: 20px;
}
.add {
  display: flex;
  flex-direction: column;
}
.add label {
  margin: 10px auto;
}
.button {
  width: 200px;
  margin: 0 auto;
  border: none;
  padding: 7px 12px;
  border-radius: 5px;
}

</style>
