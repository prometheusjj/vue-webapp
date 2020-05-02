<template>
  <div class="list">
    <div class="city-item">
      <p>定位/附近城市</p>
      <div v-for="item in mapCities" :key="item.id" @click="toHome(item.name)">{{item.name}}</div>
    </div>

    <div class="city-item">
      <p>已开通周边游站点</p>
      <div v-for="item in cities" :key="item.id" @click="toHome(item.name)">{{item.name}}</div>
    </div>

    <div class="city-item">
      <p>热门玩乐城市</p>
      <div v-for="item in hotCities" :key="item.id" @click="toHome(item.name)">{{item.name}}</div>
    </div>
  </div>
</template>

<script>
import { mapMutations } from "vuex";
export default {
  data() {
    return {
      mapCities: [],
      cities: [],
      hotCities: []
    };
  },
  mounted() {
    let That = this;
    this.axios.get("http://localhost:8080/api/city.json").then(res => {
      let data = res.data.data;
      // console.log(res.data.data);
      That.mapCities = data.mapCities;
      That.cities = data.cities;
      That.hotCities = data.hotCities;
    });
  },
  methods: {
    toHome(city) {
      // console.log(city);
      this.changeCity(city);
      this.$router.push({
        path: "/"
      });
    },
    ...mapMutations(["changeCity"])
  }
};
</script>
<style scoped>
.city-item {
  margin-top: 0.3rem;
  padding-left: 0.4rem;
  color: #999;
  font-size: 0.4rem;
}
.city-item p {
  padding: 0.3rem 0;
}
.city-item div {
  display: inline-block;
  width: 2rem;
  height: 0.82rem;
  line-height: 0.82rem;
  border: 1px solid #ccc;
  border-radius: 0.2rem;
  text-align: center;
  margin-right: 0.4rem;
  margin-bottom: 0.2rem;
  box-sizing: border-box;
}
</style>