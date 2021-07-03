<template>
  <div id="app">
    <app-header :seller="seller"></app-header>
    <div class="tab">
      <div
        :class="{ active: isActive === 1 }"
        class="tab-item"
        @click="changeTab('goods', 1)"
      >
        商品
      </div>
      <div
        :class="{ active: isActive === 2 }"
        class="tab-item"
        @click="changeTab('ratings', 2)"
      >
        评论
      </div>
      <div
        :class="{ active: isActive === 3 }"
        class="tab-item"
        @click="changeTab('seller', 3)"
      >
        商家
      </div>
    </div>
    <component :is="currentTab"></component>
  </div>
</template>

<script>
import AppHeader from "./components/header/hheader.vue";
import goods from "./components/goods/goods";
import ratings from "./components/ratings/ratings";
import seller from "./components/seller/seller";
import axios from "axios";
import "./common/stylus/index.styl";

export default {
  name: "App",
  components: {
    AppHeader,
    goods,
    ratings,
    seller,
  },
  data() {
    return {
      currentTab: "goods",
      isActive: 1,
      seller: {},
    };
  },
  methods: {
    changeTab(tabName, i) {
      (this.currentTab = tabName), (this.isActive = i);
    }, 
    getInfor() {
      axios.get("/api/seller").then((res) => {
        console.log(res.data.data);
        this.seller = res.data.data;
      });
    },
  },
  mounted() {
    this.getInfor();
  },
};
</script>

<style lang="stylus" scoped>
@import './common/stylus/mixin.styl';

.tab {
  display: flex;
  width: 100%;
  height: 40px;
  line-height: 40px;
  // border-bottom: 1px solid rgba(7, 17, 27, 0.1)
  border-1px(rgba(7, 17, 27, 0.1));

  .tab-item {
    flex: 1;
    text-align: center;
  }

  .active {
    color: red;
    // & > div
    // display: block
    // font-size: 14px
    // color: rgb(77, 85, 93)
    // &.active
    // color: rgb(240, 20, 20)
  }
}
</style>
