<template>
  <div class="tab-bar-item" @click="itemClick">
    <slot v-if="!isActivity" name="item-icon-active"></slot>
    <slot v-else name="item-icon"></slot>
    <div :style="activeStyle">
      <slot name="item-text"></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    path: String,
    activecolor: {
      type: String,
      default: "red"
    }
  },
  data() {
    return {
      //   isActivity: true
    };
  },
  computed: {
    isActivity() {
      return this.$route.path.indexOf(this.path) !== -1;
    },
    activeStyle() {
      return this.isActivity ? { color: this.activecolor } : {};
    }
  },
  methods: {
    itemClick() {
      if (this.$route.path !== this.path) {
        this.$router.replace(this.path);
      }
    }
  }
};
</script>

<style scoped>
.tab-bar-item {
  flex: 1;
  height: 49px;
  text-align: center;
  font-size: 0.6em;
}
.tab-bar-item img {
  widows: 26px;
  height: 26px;
  margin-top: 4px;
  vertical-align: middle;
}
.active {
  color: rgb(0, 183, 255);
}
</style>