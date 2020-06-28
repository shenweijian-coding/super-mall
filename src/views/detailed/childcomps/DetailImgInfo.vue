<template>
  <div v-if="Object.keys(detailinfo).length!=0">
    <div class="desc-info">
      <div class="bordertop"></div>
      <div class="desc">{{detailinfo.desc}}</div>
      <div class="borderbottom"></div>
    </div>
    <div class="key">{{detailinfo.detailImage[0].key}}</div>
    <div class="detailimage">
      <img :src="item" v-for="(item,index) in detailinfo.detailImage[0].list" :key="index" alt />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    detailinfo: {
      type: Object,
      default() {
        return {};
      }
    }
  }
};
</script>

<style>
.bordertop {
  width: 30%;
  background: #000;
  height: 1px;
  float: left;
  margin-left: 20px;
  position: relative;
}
.borderbottom {
  width: 30%;
  background: #000;
  height: 1px;
  float: right;
  margin-right: 20px;
  position: relative;
}
.bordertop::before,
.borderbottom::after {
  content: "";
  position: absolute;
  width: 5px;
  height: 5px;
  background: rgb(37, 37, 37);
  border-radius: 50%;
}
.detailimage img {
  width: 100vw;
}
.desc-info {
  margin-top: 20px;
}
.key {
  margin-top: 30px;
  margin-left: 20px;
}
.desc {
  padding: 20px;
}
.detailimage {
  margin-top: 20px;
}
</style>