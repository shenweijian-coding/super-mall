<template>
  <div>
    <nav-bar>
      <div slot="left" class="back" @click="backClick">
        <img src="../../../assets/img/common/back.svg" alt />
      </div>
      <div class="title" slot="center">
        <div
          v-for="(item,index) in titleitem"
          :key="index"
          class="title-item"
          :class="{active:index===curindex}"
          @click="titleClick(index)"
        >{{item}}</div>
      </div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";

export default {
  components: { NavBar },

  data() {
    return {
      titleitem: ["商品", "参数", "评论", "推荐"],
      curindex: 0
    };
  },
  methods: {
    titleClick(index) {
      this.curindex = index;
    },
    backClick() {
      this.$router.back();
    }
  }
};
</script>

<style scoped>
.title {
  display: flex;
}
.title-item {
  flex: 1;
  font-size: 16px;
}
.active {
  color: red;
}
.back img {
  margin-top: 12px;
}
</style>