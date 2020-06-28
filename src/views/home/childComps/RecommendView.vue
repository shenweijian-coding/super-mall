<template>
  <div class="recommend">
    <div v-for="item in recommends">
      <a :href="item.link">
        <img :src="item.image" alt />
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    recommends: {
      type: Array,
      default() {
        return [];
      }
    }
  }
};
</script>

<style>
.recommend {
  display: flex;
  text-align: center;
  font-size: 14px;
  padding: 15px 0 14px;
  border-bottom: 8px solid #eee;
}
.recommend > div {
  flex: 1;
}
.recommend img {
  height: 55px;
  margin-bottom: 10px;
}
</style>