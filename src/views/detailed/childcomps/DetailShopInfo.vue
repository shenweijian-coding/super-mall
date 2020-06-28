<template>
  <div>
    <div class="shopinfo">
      <img :src="shop.logo" alt />
      <p>{{shop.name}}</p>
    </div>
    <div class="shop-info">
      <div>
        <div class="shopcount">
          <div class="fans">
            <p>{{shop.fans}}</p>
            <p>总销量</p>
          </div>
          <div class="count">
            <p>{{shop.goodsCount}}</p>
            <p>全部宝贝</p>
          </div>
        </div>
      </div>
      <div class="shopscore">
        <div v-for="(item,index) in shop.score" :key="index" class="score">
          <div>{{item.name}}</div>
          <div>{{item.score}}</div>
          <div class="height" :class="{active:item.isBetter}">{{height=item.isBetter?'高':'低'}}</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      height: "高"
    };
  },
  methods: {
    scoreClick(flag) {
      this.height = flag ? "高" : "低";
    }
  },
  created() {},
  props: {
    shop: {
      type: Object,
      default() {
        return {};
      }
    }
  }
};
</script>

<style scoped>
.shopinfo {
  margin-top: 20px;
  padding: 16px;
}
.shopinfo img {
  width: 50px;
  border-radius: 50%;
  border: 1px solid rgb(196, 196, 196);
  float: left;
}
.shopinfo p {
  display: inline-block;
  line-height: 50px;
  margin-left: 20px;
  font-size: 18px;
}
.shopcount {
  display: flex;
  text-align: center;
  margin-top: 40px;
}
.fans,
.count {
  margin-left: 20px;
}
.fans p:nth-child(1),
.count p:nth-child(1) {
  font-size: 26px;
  margin-bottom: 16px;
}

.shop-info {
  display: flex;
}
.shopscore {
  margin-left: 28px;
}
.shopscore .score * {
  float: left;
  margin: 16px 0;
}
.height {
  width: 18px;
  background: rgb(0, 168, 50);
  color: #fff;
  text-align: center;
}

.score div:nth-child(2) {
  width: 60px;
  margin-left: 10px;
}
.active {
  width: 18px;
  background: rgb(168, 0, 0);
  color: #fff;
  text-align: center;
}
</style>