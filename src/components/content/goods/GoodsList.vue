<template>
  <main class="goods">
    <!-- <div v-for="(item,index) in goods" class="goods-item" :key="index">
      <a :href="item.link">
        <img :src="item.show.img" @load="imgLoad" />
        <div class="goodsinfo">
          <p>{{item.title}}</p>
          <span>{{item.price}}元</span>
        </div>
      </a>
    </div>-->
    <good-list-view v-for="item in goods" :goodsitem="item" @imgLoadend="imgLoadend"></good-list-view>
  </main>
</template>
<script>
import GoodListView from "./GoodListView";
export default {
  components: {
    GoodListView
  },
  props: {
    goods: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  methods: {
    imgLoadend() {
      this.$emit("imgLoadend");
    }
  }
};
</script>

<style scoped>
.goods {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;
}
</style>