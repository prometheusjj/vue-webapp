<template>
  <div class="spike">
    <swiper :options="swiperOption">
      <!-- slides -->

      <swiper-slide v-for="item in spikeList" :key="item.id">
        <div class="spike-content" @click="toDetails(item)">
          <div class="spike-top">
            <img src="@/assets/img/spike1.png" />
            <span>距离结束</span>
            <count-down
              :currentTime="item.startTime"
              :startTime="item.startTime"
              :endTime="item.endTime"
              :dayTxt="'天'"
              :hourTxt="':'"
              :minutesTxt="':'"
              :secondsTxt="''"
            ></count-down>
          </div>
          <div class="spike-bottom">
            <img :src="item.imgUrl" />
            <div class="bottom-title">
              <p>{{item.title}}</p>
              <div class="bottom-price">
                <span>￥{{item.price}}</span>
                <p>剩下{{item.num}}个</p>
              </div>
            </div>
          </div>
        </div>
      </swiper-slide>
      <!-- Optional controls -->
      <div class="swiper-pagination" slot="pagination"></div>
    </swiper>
  </div>
</template>

<script>
import CountDown from "vue2-countdown";
export default {
  props: ["spikeList"],
  data() {
    return {
      //   props: ["spikeList"],
      // spikeList: [
      //   {
      //     id: 0,
      //     startTime: 1588148038641,
      //     endTime: 1588175112817,
      //     imgUrl: "http://localhost:8080/img/spike2.jpg",
      //     title: "大萨京东卡待调度豆瓣读书腹背受敌的近似的大萨达是滴啊",
      //     price: 80,
      //     num: 35
      //   },
      //   {
      //     id: 1,
      //     startTime: 1588148038641,
      //     endTime: 1588175112817,
      //     imgUrl: "http://localhost:8080/img/spike2.jpg",
      //     title: "大萨京东卡待调度豆瓣读书腹背受敌的近似的大萨达是滴啊",
      //     price: 80,
      //     num: 35
      //   },
      //   {
      //     id: 2,
      //     startTime: 1588148038641,
      //     endTime: 1588175112817,
      //     imgUrl: "http://localhost:8080/img/spike2.jpg",
      //     title: "大萨京东卡待调度豆瓣读书腹背受敌的近似的大萨达是滴啊",
      //     price: 80,
      //     num: 35
      //   }
      // ],

      swiperOption: {
        pagination: {
          el: ".swiper-pagination"
        }
      }
    };
  },
  components: {
    CountDown
  },
  methods: {
    countDownS_cb: function(x) {
      console.log(x);
    },
    countDownE_cb: function(x) {
      console.log(x);
    },
    toDetails(item) {
      this.$router.push({
        path: "/details",
        query: {
          item
        }
      });
    }
  },
  mounted() {
    // console.log(new Date().getTime() + 5 * 24 * 60 * 3600);
  }
};
</script>

<style scoped>
.spike {
  width: 100%;
  height: 4.377777rem;
}
.spike-content {
  padding: 0.3rem;
}
.spike-top {
  width: 100%;
  height: 1.2933333rem;
  display: flex;
  align-items: center;
  font-size: 0.35rem;
}
.spike-top img {
  height: 0.41333333rem;
  width: 1.89333333rem;
}
.spike-top span {
  margin-left: 0.15rem;
}
.spike-top > div {
  margin-left: 0.15rem;
}
.spike-top >>> div span {
  margin-left: 0.15rem;
  color: #fff;
  border-radius: 0.1rem;
  background: #8b8b8b;
  padding: 0 0.1rem;
}
.spike-bottom {
  display: flex;
  justify-content: space-between;
}
.spike-bottom img {
  width: 3.093333rem;
  height: 2.12rem;
}
.spike-bottom .bottom-title {
  width: 5.86rem;
}

.bottom-title p {
  line-height: 0.38rem;
  font-size: 0.35rem;
  color: #333;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 2;
  overflow: hidden;
}
.bottom-price {
  margin-top: 0.8rem;
  display: flex;
  justify-content: space-between;
  font-size: 0.35rem;
}
.bottom-price p {
  padding: 0.1rem;
  border: 1px solid #444;
  border-radius: 0.1rem;
  background: #fed101;
}

.swiper-container {
  overflow: visible;
}
.swiper-pagination >>> .swiper-pagination-bullet-active {
  background: orange;
}
.swiper-pagination-fraction,
.swiper-pagination-custom,
.swiper-container-horizontal > .swiper-pagination-bullets {
  bottom: -0.8rem;
}
</style>