<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-contral
      :titles="['精选','流行','爆款']"
      v-show="isfixdtab"
      class="fixtab"
      @tabClick="tabClick"
      ref="tabcontrol1"
    ></tab-contral>
    <back-top @click.native="backClick" v-show="isbacktopshow"></back-top>
    <scroll
      class="content"
      ref="backtop"
      :proscroll="3"
      @getposition="getposition"
      :pull-up-load="true"
      @pullingUp="loadmore"
    >
      <home-swiper class="banner" :banners="banners"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <tab-contral
        :titles="['精选','流行','爆款']"
        class="catatory"
        @tabClick="tabClick"
        ref="tabcontrol2"
      ></tab-contral>
      <goods-list :goods="curitem" @imgLoadend="imgLoadend"></goods-list>
    </scroll>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar.vue";
import TabContral from "components/content/tabControl/TabContral.vue";
import GoodsList from "components/content/goods/GoodsList.vue";
import BackTop from "components/content/backtop/BackTop";
import HomeSwiper from "./childComps/HomeSwiper";
import RecommendView from "./childComps/RecommendView";
import { getHomeMultidata, getHomeGoods } from "network/home.js";
//滑动better-scroll
import Scroll from "components/common/scroll/Scroll.vue";
export default {
  components: {
    NavBar,
    HomeSwiper,
    RecommendView,
    TabContral,
    GoodsList,
    Scroll,
    BackTop
  },
  data() {
    return {
      flag: "pop",
      banners: [],
      recommends: [],
      isbacktopshow: false,
      tabofoffset: null,
      isfixdtab: false,
      goods: {
        pop: { page: 0, list: [] },
        new: { page: 0, list: [] },
        sell: { page: 0, list: [] }
      }
    };
  },

  created() {
    this.getHomemultidata();
    this.getHomegoods("pop");
    this.getHomegoods("new");
    this.getHomegoods("sell");
  },
  computed: {
    curitem() {
      return this.goods[this.flag].list;
    }
  },
  mounted() {},
  methods: {
    //更改图片刷新频率
    imgLoadend() {
      this.$refs.backtop.scroll.refresh();
    },
    //封装debounce方法
    // debounce(func, delay) {
    //   let timer = null;
    //   return function(...args) {
    //     if (timer) clearTimeout(timer);
    //     timer = setInterval(() => {
    //       func.apply(this, args);
    //     }, delay);
    //   };

    //网络请求方法
    getHomemultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list;
        this.recommends = res.data.recommend.list;
      });
    },
    getHomegoods(type) {
      const page = this.goods[type].page + 1;
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list);
        this.goods[type].page += 1;
        this.$refs.backtop.scroll.finishPullUp();
      });
    },
    //时间监听
    tabClick(index) {
      switch (index) {
        case 0:
          this.flag = "pop";
          break;
        case 1:
          this.flag = "new";
          break;
        case 2:
          this.flag = "sell";
          break;
      }
      this.$refs.tabcontrol1.cur = index;
      this.$refs.tabcontrol2.cur = index;
    },
    //监听向上返回
    backClick() {
      this.$refs.backtop.scroll.scrollTo(0, 0, 500);
    },
    getposition(position) {
      this.isbacktopshow = -position.y > 1000;
      this.isfixdtab = -position.y > 320;
    },
    loadmore() {
      this.getHomegoods(this.flag);
      this.$refs.backtop.scroll.refresh();
    }
  }
};
</script>

<style scoped>
#home {
  background: #fff;
  height: 100vh;
  position: relative;
}
.home-nav {
  background-color: var(--color-tint);
  color: white;

  /* position: fixed;
  z-index: 9;
  left: 0;
  right: 0; */
}

.content {
  position: absolute;
  top: 44px;
  bottom: 49px;
  right: 0;
  left: 0;
  overflow: hidden;
}
.fixtab {
  position: relative;
  z-index: 9;
}
</style>