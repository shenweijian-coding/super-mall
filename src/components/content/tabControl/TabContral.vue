<template>
  <div class="tabcontrol">
    <div
      v-for="(item,index) in titles"
      @click="itemClick(index)"
      class="tab-control-item"
      :class="{active:index===cur}"
    >
      <span :class="{lineactive:index===cur}">{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    titles: {
      type: Array,
      default() {
        return [];
      }
    }
  },
  data() {
    return {
      cur: 0
    };
  },
  methods: {
    itemClick(index) {
      this.cur = index;
      this.$emit("tabClick", index);
    }
  }
};
</script>

<style>
.tabcontrol {
  display: flex;
  text-align: center;
  height: 44px;
  line-height: 44px;
  background: #fff;
}
.tab-control-item {
  flex: 1;
}
.tab-control-item span {
  padding: 5px;
}
.active {
  color: hotpink;
}
.lineactive {
  border-bottom: 2px solid hotpink;
}
</style>