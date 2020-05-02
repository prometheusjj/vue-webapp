<template>
  <div class="home">
    <Banner />
    <Icons />
    <Tabs />
    <Scroll />
    <Swiper />
    <Spike :spikeList="spikeList" />
    <Like :likeList="likeList" />
    <Footer />
  </div>
</template>

<script>
import { mapState } from "vuex";
import Banner from "./Banner";
import Icons from "./Icons";
import Tabs from "./Tabs";
import Scroll from "./Scroll";
import Swiper from "./Swiper";
import Spike from "./Spike";
import Like from "./Like";
import Footer from "./Footer";

export default {
  components: {
    Banner,
    Icons,
    Tabs,
    Scroll,
    Swiper,
    Spike,
    Like,
    Footer
  },
  data() {
    return {
      spikeList: [],
      likeList: [],
      changeCity: ""
    };
  },
  methods: {
    http() {
      let That = this;
      this.axios.get("http://localhost:8080/api/dataHome.json").then(res => {
        let data = res.data.data;
        That.spikeList = data[0].spikeList;
        // console.log(data[0].spikeList);
        // console.log(That.spikeList);
        data.forEach((item, index) => {
          if (item.city == That.cityName) {
            That.spikeList = item.spikeList;
            That.likeList = item.likeList;
          }
          // console.log(index);
        });
      });
    }
  },
  mounted() {
    this.http();
    // console.log(this.spikeList);
  },
  activated() {
    if (this.changeCity != this.cityName) {
      this.http();
      this.changeCity = this.cityName;
    }
  },
  computed: {
    ...mapState(["cityName"])
  }
};
</script>

<style scoped>
.home {
  overflow: hidden;
}
</style>