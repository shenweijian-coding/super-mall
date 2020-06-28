<template>
  <div class="goods-item" @click="itemClick">
    <img :src="showimage" @load="imgLoad" />
    <div class="goodsinfo">
      <p>{{goodsitem.title}}</p>
      <span>{{goodsitem.price}}元</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    goodsitem: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  computed: {
    showimage() {
      return this.goodsitem.image || this.goodsitem.show.img;
    }
  },
  methods: {
    imgLoad() {
      this.$emit("imgLoadend");
    },
    itemClick() {
      this.$router.push("/detail/" + this.goodsitem.iid);
    }
  }
};
</script>

<style scoped>
.goods-item {
  width: 50%;
  padding: 10px;
  position: relative;
}
.goods-item .goodsinfo {
  font-size: 0.8em;
  color: #555;
  overflow: hidden;
}
.goodsinfo span {
  color: red;
  position: absolute;
  left: 36%;
}
.goodsinfo p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.goods-item img {
  width: 100%;
  border-radius: 3px;
}
</style>