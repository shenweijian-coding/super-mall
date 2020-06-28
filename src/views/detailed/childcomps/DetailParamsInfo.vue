<template>
  <div v-if="Object.keys(itemparams).length!=0">
    <div class="itemparams">
      <table v-for="(table,indey) in itemparams.rule.tables" :key="indey">
        <tr v-for="(tr,index) in table" :key="index">
          <td v-for="(td,indez) in tr" :key="indez">{{td}}</td>
        </tr>
      </table>
    </div>
    <div class="info">
      <table>
        <tr v-for="(tr,index) in itemparams.info.set" :key="index">
          <td v-for="(td,indey) in tr" :key="indey">{{td}}</td>
        </tr>
      </table>
    </div>
    <div class></div>
  </div>
</template>

<script>
export default {
  props: {
    itemparams: {
      type: Object,
      default() {
        return {};
      }
    }
  }
};
</script>

<style scoped>
.itemparams table {
  width: 100vw;
  border-collapse: collapse;
  text-align: center;
  margin-top: 20px;
  color: #555;
}
.itemparams table tr td {
  padding: 20px;
  border: 1px solid #ccc;
}
.itemparams table tr td:nth-child(1) {
  width: 26%;
}

.info table {
  width: 100vw;
  border-collapse: collapse;

  margin-top: 20px;
  color: #555;
}
.info table tr {
  border: 1px solid #ccc;
}
.info table td {
  padding: 12px;
  color: #555;
}
.info table tr td:nth-child(1) {
  width: 18%;
}
.info table tr td:nth-child(2) {
  color: rgb(223, 0, 0);
}
</style>