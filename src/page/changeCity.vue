<template>
  <div class="page-changeCity">
    <el-row class="">
      <province />
    </el-row>
    <el-row>
      <hot title="热门城市:" :list="hotList" />
    </el-row>
    <el-row>
      <hot title="最近访问:" :list="recentList" />
    </el-row>
    <el-row>
      <categroy />
    </el-row>
  </div>
</template>

<script>
import Province from '@/components/changeCity/province.vue'
import Hot from '@/components/changeCity/hot.vue'
import Categroy from '@/components/changeCity/categroy.vue'
import api from '@/api/index.js'
export default {
  data () {
    return {
      hotList: [],
      recentList: []
    }
  },
  created () {
    api.getHotCity().then(res => {
      this.hotList = res.data.data.map(item => item.name)
    })
    api.getRecentCity().then(res => {
      this.recentList = res.data.data.map(item => item.name)
    })
  },
  components: {
    Province,
    Hot,
    Categroy
  }
}
</script>
