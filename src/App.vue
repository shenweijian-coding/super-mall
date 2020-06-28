<template>
  <div id="app">
    <keep-alive exclude="Detailed">
      <router-view />
    </keep-alive>
    <main-tab-bar class="maintabbar" />
  </div>
</template>

<script>
import MainTabBar from "./components/content/MainTabBar/MainTabBar";

export default {
  name: "App",
  components: {
    MainTabBar
  }
};
</script>

<style>
@import "./assets/css/base.css";
</style>
