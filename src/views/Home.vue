<template>
  <div id="home">
    <!-- 组件懒加载 -->
    <lazy-component>
      <!-- swipe轮播图 -->
      <div class="swipe" v-if="this.banners">
        <van-swipe :autoplay="3000" width="100%" height="2.18rem">
          <van-swipe-item v-for="(image, index) in banners" :key="index">
            <img v-lazy="image.pictureUrl" />
          </van-swipe-item>
        </van-swipe>
      </div>

      <!-- 菜单栏 -->
      <div class="menu" v-if="this.menus">
        <van-grid :gutter="10" :border="false">
          <van-grid-item
            v-for="item in menus"
            :key="item.navIndex"
            :icon="item.pictureUrl"
            :text="item.navName"
            @click="toUrl(item.hrefValue)"
          />
        </van-grid>
      </div>

      <!-- 餐馆名菜在家做 -->
      <div class="goodFood">
        <van-image
          width="100%"
          height="100%"
          src="https://img11.yiguoimg.com/d/items/2020/200331/9288740194363519_1125x344.jpg?w=1125&h=344"
        />
      </div>

      <!-- 易果快报 -->
      <div class="news" v-if="this.news">
        <van-row>
          <van-col span="6">
            <img src="//img06.yiguoimg.com/e/web/161222/018522/134216/news.png" />
          </van-col>
          <van-col span="18">
            <div class="slider-content">
              <van-swipe style="height: 100%;" :autoplay="3000" :show-indicators="false" vertical>
                <van-swipe-item v-for="item in news" :key="item.fastReportId">
                  <span class="slider-text">{{item.fastReportTitle}}</span>
                </van-swipe-item>
              </van-swipe>
            </div>
          </van-col>
        </van-row>
      </div>

      <!-- 重磅推荐 -->
      <div class="tuijian" v-if="this.tuijian">
        <van-row>
          <van-col span="24">
            <van-image
              v-for="item in tuijian"
              :key="item.adPictures.adPictureId"
              width="100%"
              lazy-load
              :src="item.adPictures.pictureUrl"
            />
          </van-col>
        </van-row>
      </div>

      <!-- 一口好锅 -->
      <div class="group-floor">
        <div class="floor-img">
            <img src="https://img12.yiguoimg.com/d/items/2020/200306/9288740052740198_1125x652.jpg?w=1125&h=652" alt="">
        </div>
      </div>
    </lazy-component>
  </div>
</template>

<script>
import Vue from "vue";
import { Toast, Overlay, Button, Icon, Swipe, SwipeItem, Lazyload, Grid, GridItem, Image } from "vant";
import axios from "axios";
Vue.use(Toast).use(Overlay).use(Button).use(Icon).use(Swipe).use(SwipeItem).use(Grid).use(GridItem).use(Image).use(Lazyload, { lazyComponent: true });

export default {
  methods: {
    toUrl(hrefValue) {
      console.log(hrefValue);
    }
  },
  data() {
    return {
      show: true,
      banners: null,
      menus: null,
      news: null,
      tuijian: null,
      haoguo:null,
      showImg:
        "https://img11.yiguoimg.com/d/items/2020/200331/9570215171106943_896x1086.png"
    };
  },
  async created() {
    // axios的get数据请求 并且赋值
    await axios.get("/json/Home/home-top.json").then(res => {
      let data = res.data[0];
      let pic = res.data[1];
      // banners赋值
      this.banners = data.carouselPictures;
      // menu赋值
      this.menus = data.navComponentList;
      // news开宝赋值
      this.news = data.fastReportsList;
      // tuijian赋值
      this.tuijian = pic;
      // console.log(this.tuijian);
    });

    Toast({
      message: "加载中...",
      icon: "https://img07.yiguoimg.com/e/web/170113/01851/110053/1.gif",
      duration: 500
    });
  }
};
</script>

<style lang="scss" scoped>
.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
.block {
  width: 3rem;
  height: 3.6rem;
  position: relative;
  .van-icon-close {
    position: absolute;
    right: 0;
    top: -15px;
  }
  img {
    width: 100%;
    height: 100%;
  }
}
// 轮播图
.swipe {
  width: 100%;
  height: 2.18rem;
  position: relative;
  img {
    width: 100%;
    height: 2.18rem;
  }
  ::v-deep {
    .van-swipe__indicators {
      bottom: 40px;
    }
  }
}
// 菜单栏
.menu {
  ::v-deep {
    .van-grid {
      padding-top: 10px;
      padding-bottom: 10px;
      .van-grid-item {
        padding-right: 0 !important;
        .van-grid-item__content {
          padding: 0;
          .van-grid-item__icon {
            width: 90px;
            height: 63px;
            text-align: center;
            img {
              width: 62px;
              height: 62px;
            }
          }
          .van-grid-item__text {
            margin-top: 0;
            color: rgb(51, 51, 51);
            font-size: 14px;
          }
        }
      }
    }
  }
}

.goodFood {
  width: 100%;
  height: 1.15rem;
}

// 易果快报
.news {
  width: 100%;
  height: 0.33rem;
  border-top: 1px solid #f4f4f4;
  .van-row {
    width: 100%;
    height: 100%;
    .van-col {
      height: 100%;
      position: relative;
      img {
        position: absolute;
        width: 0.68rem;
        height: 0.13rem;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
      }
    }
    .van-col--6 {
      border-right: 1px solid #f4f4f4;
    }
    .van-col--18 {
      .slider-content {
        width: 100%;
        height: 100%;
        ::v-deep {
          .van-swipe__track {
            height: 100% !important;
            .slider-text {
              display: flex;
              width: 100%;
              height: 100%;
              font-size: 12px;
              margin-left: 10px;
              flex-direction: row;
              align-items: center;
              justify-content: flex-start;
            }
          }
        }
      }
    }
  }
}

// 重磅推荐
.tuijian {
  width: 100%;
  height: 3.6rem;
  .van-row {
    .van-col {
      ::v-deep {
        .van-image {
          display: block;
        }
      }
    }
  }
}

.group-floor{
  width: 100%;
  height: 4rem;
  .floor-img{
    width: 100%;
    img{
      width: 100%;
    }
  }
}
</style>
