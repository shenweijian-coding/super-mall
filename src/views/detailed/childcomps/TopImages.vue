<template>
  <div class="topimages">
    <swiper>
      <swiper-item v-for="item in topImages">
        <img :src="item" alt />
      </swiper-item>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperItem } from "components/common/swiper/index.js";
export default {
  components: {
    Swiper,
    SwiperItem
  },
  props: {
    topImages: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  created() {}
};
</script>

<style scoped>
.topimages {
  height: 300px;
  overflow: hidden;
}
</style>