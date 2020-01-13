<template>
  <div class="categroy">
    <dl class="m-categroy">
      <dt>按拼音字母选择:</dt>
      <dd v-for="(item, index) in list" :key="index">
        <a :href="'#city-' + item">{{item}}</a>
      </dd>
    </dl>
    <dl class="m-categroy-section" :id="'city-' + index" v-for="(item, index) in cityGroup" :key="index">
      <dt>{{index}}</dt>
      <dd>
        <span v-for="city in item" :key="city.id" @click="changeCity(city)">{{city.name}}</span>
      </dd>
    </dl>
  </div>
</template>
<script>
import api from '@/api/index.js'
export default {
  data() {
    return {
      list: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'.split(''),
      cityList: [],
      cityGroup: {}
    }
  },
  created () {
    api.getCityList().them(res => {
      var obj = {}
      res.data.data.forEach((item, index) => {
        if(obj[item.firstChar.toUpperCase()]){
          obj[item.firstChar.toUpperCase()] = []
        }
        obj[item.firstChar.toUpperCase()].push(item)
      })
      this.cityGroup = obj
    })
  },
  methods: {
    changeCity (item) {
      this.$store.dispatch('setPosition', item)
      this.$router.push({name: 'index'})
    }
  }
}
</script>
<style lang="scss">
  @import '@/assets/css/changeCity/categroy.scss'
</style>
