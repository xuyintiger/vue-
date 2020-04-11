<template>
  <div class="list">
    <div class="topbar line-bottom">
      <ul>
        <li
          v-for="data in topbarList"
          :key="data"
          @click="topbarChange(data)"
          :class="{ active: data === current }"
        >
          {{ data }}
        </li>
      </ul>
    </div>
    <div class="itemlist" v-if="productList">
    </div>
    <div v-if="!productList" class="message">
      <img
        src="//img07.yiguoimg.com/d/web/180315/013111/212501/noting@3x.png"
        alt=""
      />
      <p>抱歉没有找到您想要的商品</p>
    </div>
    <div class="car" @click="test">
      
    </div>
  </div>
</template>

<script>
import { mapMutations, mapState } from "vuex";
import { getClassiftList } from "@/api/JsonRequest";
import Vue from "vue";
import { Toast } from "vant";
Vue.use(Toast);

export default {
  data() {
    return {
      topbarList: ["销量", "新品", "价格"],
      data: "销量",
      current: "销量",
      productList: null,
      productCarList: [],
    }
  },
  props: ["id", "index"],
 
};
</script>

<style lang="scss" scoped>
* {
  padding: 0;
  margin: 0;
}

.list {
  .topbar {
    position: fixed;
    left: 0;
    right: 0px;
    background-color: #fff;
    z-index: 9;
    ul {
      display: flex;
      justify-content: space-around;
      li {
        font-size: 15px;
        width: 33.33%;
        text-align: center;
        padding: 10px 0;
      }
    }
    .active {
      border-bottom: 2px solid #11b57c;
      box-sizing: border-box;
      color: #11b57c;
    }
  }
  .line-bottom:after {
    content: "";
    position: absolute;
    left: 0;
    width: 100%;
    height: 1px;
    background: #ddd;
    -webkit-transform: scaleY(0.5);
    transform: scaleY(0.5);
    -webkit-transform-origin: 0 100%;
    transform-origin: 0 100%;
  }

 
  .message {
    position: relative;
    top: 100px;
    text-align: center;
    img {
      width: 108px;
      height: 108px;
    }
    p {
      font-size: 15px;
      color: #808080;
    }
  }
  .car {
    background: url("http://img05.yiguoimg.com/d/web/180508/01311/150610/cart1.png")
      no-repeat;
    z-index: 100;
    position: relative;
    display: block;
    width: 34px;
    height: 34px;
    background-size: 100%;
    position: fixed;
    bottom: 140px;
    right: 30px;
   
  }
}
</style>
