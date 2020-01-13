<template>
  <div class="m-product-categroy">
    <dl class="classic">
      <dt>分类</dt>
      <dt>全部</dt>
      <dd v-for="item in classicList" :key="item.type">
        <m-select :name="item.title" :list="item.sub_title" />
      </dd>
    </dl>
    <dl class="classic">
      <dt>区域</dt>
      <dt>全部</dt>
      <dd v-for="item in areaList" :key="item.type">
        <m-select :name="item.title" :list="item.sub_title" />
      </dd>
    </dl>
  </div>
</template>
<script>
import MSelect from './select'
export default {
  data() {
    return {
      classicList: [
        {
          title: "美食",
          type: "food",
          sub_title: [
            {
              name: "日本菜",
              id: "Japan"
            },
            {
              name: "饮品店",
              id: "drink"
            },
            {
              name: "面包甜点",
              id: "cake"
            }
          ]
        },
        {
          title: "酒店住宿",
          type: "hotel",
          sub_title: [
            {
              name: "温泉酒店",
              id: "hot_spring"
            },
            {
              name: "经济酒店",
              id: "economy"
            },
            {
              name: "高端酒店",
              id: "high"
            }
          ]
        },
      ],
      areaList: [
        {
          title: "推荐商圈",
          sub_title: [
            {
              name: "望京",
              id: 120000
            },
            {
              name: "昌平",
              id: 122222
            }

          ]
        }
      ]
    };
  },
  components: {
    MSelect
  }
};
</script>
