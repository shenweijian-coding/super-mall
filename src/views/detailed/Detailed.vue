<template>
  <div>
    <div class="detail-bg">
      <div class="detailbar">
        <detail-nav-bar class="detailbar"></detail-nav-bar>
      </div>

      <top-images :topImages="topImages"></top-images>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      <detail-img-info :detailinfo="detailInfo"></detail-img-info>
      <detail-params-info :itemparams="itemparams"></detail-params-info>
      <detail-comment-info :commentInfo="commentInfo"></detail-comment-info>
      <goods-list :goods="recommends"></goods-list>
      <detail-bottom-bar></detail-bottom-bar>
    </div>
  </div>
</template>

<script>
import DetailNavBar from "./childcomps/DetailNavBar";
import { getDetailItem, Goods, Shop, getRecommend } from "network/detail.js";
import Scroll from "components/common/scroll/Scroll.vue";
import topImages from "./childcomps/TopImages";
import DetailBaseInfo from "./childcomps/DetailBaseInfo";
import DetailShopInfo from "./childcomps/DetailShopInfo";
import DetailBottomBar from "./childcomps/DetailBottomBar";
import DetailImgInfo from "./childcomps/DetailImgInfo";
import DetailParamsInfo from "./childcomps/DetailParamsInfo";
import DetailCommentInfo from "./childcomps/DetailCommentInfo";
import GoodsList from "components/content/goods/GoodsList";
export default {
  name: "Detailed",
  components: {
    DetailNavBar,
    topImages,
    DetailBaseInfo,
    DetailShopInfo,
    DetailBottomBar,
    DetailImgInfo,
    Scroll,
    DetailParamsInfo,
    DetailCommentInfo,
    GoodsList
  },
  data() {
    return {
      iid: null,
      topImages: [],
      goods: {},
      shop: {},
      detailInfo: {},
      itemparams: {},
      commentInfo: {},
      recommends: []
    };
  },

  created() {
    this.iid = this.$route.params.id;
    getDetailItem(this.iid).then(res => {
      const data = res.result;

      this.topImages = data.itemInfo.topImages;
      console.log(res);

      this.goods = new Goods(
        data.itemInfo,
        data.columns,
        data.shopInfo.services
      );
      this.shop = new Shop(data.shopInfo);
      this.detailInfo = data.detailInfo;
      this.itemparams = data.itemParams;
      if (data.rate.cRate !== 0) {
        this.commentInfo = data.rate.list[0];
      }
    });
    //请求推荐数据
    getRecommend().then(res => {
      this.recommends = res.data.list;
    });
  }
};
</script>

<style>
.detail-bg {
  background: #fff;
  position: relative;
  z-index: 1;
}
.detailbar {
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  z-index: 9;
  background: #ffffff;
}
</style>