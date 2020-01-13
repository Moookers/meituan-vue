<template>
  <div class="m-istyle">
    <dl @mouseover="over" :class="nav.class">
      <dt>{{nav.title}}</dt>
      <dd
        v-for="(item,index) in nav.list"
        :key="index"
        :class="{active: kind == item.tab}"
        :data-type="item.tab"
      >{{item.text}}</dd>
    </dl>
    <ul class="ibody">
      <li v-for="(item,index) in resultsData[kind]" :key="index">
        <el-card>
          <img :src="item.image" alt />
          <div class="cbody">
            <div class="title" :title="item.title">{{item.title}}</div>
            <div class="sub-title">{{item.sub_title}}</div>
            <div class="price-info">
              <span class="current-price-wrappers">
                <span class="price-symbol numfont">￥</span>
                <span class="currentprice numfont">{{item.price}}</span>
              </span>
              <span class="sold bottom-right-info">{{item.address}}</span>
              <!-- <span class="old-price">门市价￥{{item.price_info.old_price}}</span>
              <span class="sold bottom-right-info">{{item.address}}</span> -->
            </div>
            <!-- <div class="price-info" v-else-if="!item.rentNum">
              <span class="current-price-wrappers">
                <span class="price-symbol numfont">￥</span>
                <span class="currentprice numfont">抢光了</span>
              </span>
            </div>
            <div class="price-info" v-else>
              <span class="current-price-wrappers">
                <span class="price-symbol numfont">￥</span>
                <span class="currentprice numfont">{{item.price_info.avg_price}}</span>
                <span class="units">/{{item.price_info.units}}</span>
              </span>
            </div> -->
          </div>
        </el-card>
      </li>
    </ul>
  </div>
</template>

<script>
import api from '@/api/index.js'
export default {
  props: ["nav"],
  data() {
    return {
      kind: "all",
      resultsData: {}
    };
  },
  created () {
    api.getResultsByKeywords().then(res => {
      this.resultsData = res.data.data
    })
  },
  methods: {
    over(e) {
      let dom = e.target;
      let targetName = dom.tagName.toLowerCase();
      if (targetName != "dd") {
        return false;
      }
      this.kind = dom.getAttribute("data-type");
      //动态获取数据  ajax请求
    }
  }
};
</script>

<style lang="scss">
@import "@/assets/css/index/artistic.scss";
</style>
