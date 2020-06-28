<template>
  <div ref="wrapper" class="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";
export default {
  props: {
    proscroll: 0,
    pullUpLoad: false
  },
  data() {
    return {
      scroll: null
    };
  },
  mounted() {
    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.proscroll,
      pullUpLoad: this.pullUpLoad
    });
    this.scroll.scrollTo(0, 0);
    //监听坐标事件
    // this.el = this.$refs.wrapper;
    // const scroll = new BScroll(this.el, {});
    this.scroll.on("scroll", position => {
      this.$emit("getposition", position);
    });
    //监听上拉加载更多;
    this.scroll.on("pullingUp", () => {
      this.$emit("pullingUp");
      // console.log("滚动到底部");
    });
  }
};
</script>

<style scoped>
</style>