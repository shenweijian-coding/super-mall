<template>
  <div class="iteminfo">
    <h3 class="title">{{goods.title}}</h3>
    <h1 class="newprice">{{goods.newPrice}}</h1>
    <p class="oldprice">{{goods.oldPrice}}</p>
    <div class="discount" v-if="goods.discount!=''">{{goods.discount}}</div>
    <div class="goodsinfo">
      <div v-for="item in goods.columns" :key="item">{{item}}</div>
    </div>

    <div class="services">
      <div v-for="(item,index) in goods.services" :key="index">
        <img :src="item.icon" alt />
        <p>{{item.name}}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    goods: {
      type: Object,
      default() {
        return {};
      }
    }
  }
};
</script>

<style scoped>
.title {
  font-size: 18px;
  padding: 16px 10px;
  color: rgb(17, 17, 17);
}
.newprice {
  color: red;
  margin: 0;
  display: inline-block;
  margin-left: 10px;
}
.oldprice {
  display: inline-block;
  text-decoration: line-through;
  font-size: 18px;
  color: rgb(73, 73, 73);
  margin-left: 10px;
}
.discount {
  display: inline;
  background: red;
  border-radius: 40px;
  color: #fff;
  border: 6px solid red;
  margin-left: 10px;
  font-size: 12px;
}
.goodsinfo {
  margin-top: 20px;
  display: flex;
  text-align: center;
  justify-content: space-evenly;
  padding: 0 0 14px 0;
  border-bottom: 1px solid rgb(224, 224, 224);
}
.goodsinfo > div {
  flex: 1;
  color: rgb(119, 119, 119);
  font-size: 17px;
}
.services {
  display: flex;
  text-align: center;
  justify-content: space-evenly;
  border-bottom: 6px solid rgb(241, 241, 241);
  padding: 20px;
}
.services img {
  width: 18px;
  margin: 0;
}
.services p {
  display: inline-block;
  font-size: 14px;
  margin-right: 14px;
  margin-left: 6px;
}
</style>