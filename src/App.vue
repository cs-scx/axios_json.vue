<template>
  <div id="app">
    <h1>{{ overview.name }}</h1>
    <hr />
    <b>简介：</b>
    <div class="text">
      <p>{{ overview.description }}</p>
    </div>
    <table class="table table-hover">
      <tbody>
        <tr>
          <td v-for="(item, index) in catalogue" :key="index">
            <a href="">{{ item }}</a>
          </td>
        </tr>
      </tbody>
    </table>
    <h2>成分</h2>
    <hr />
    <div class="text">
      <p>{{ ingredient }}</p>
    </div>
    <p>化学式结构：</p>
    <img
      src="https://bkimg.cdn.bcebos.com/pic/14ce36d3d539b600c2785b5deb50352ac75cb7a2?x-bce-process=image/resize,m_lfit,w_220,h_220,limit_1"
      alt=""
    />
    <h2>性状</h2>
    <hr />
    <div class="text">{{ feature }}</div>
    <h2>适应症</h2>
    <hr />
    <div class="text">
      <p>{{ adapt_symptom }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const baseURL = "http://localhost:3000/content";

export default {
  name: "App",
  data() {
    return {
      overview: "",
      catalogue: "",
      ingredient: "", //成分
      img: "",
      feature: "", //特性
      adapt_symptom: "", //适用症状
    };
  },
  async created() {
    try {
      const res = await axios.get(baseURL);
      this.overview = res.data;
      this.catalogue = this.overview.catalogue;
      this.ingredient = this.overview.data[0].ingredient;
      this.feature = this.overview.data[1].feature;
      this.adapt_symptom = this.overview.data[2].adapt_symptom;
    } catch (e) {
      console.log(e);
    }
  },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.text {
  background-color: rgb(238, 238, 238);
  padding: 10px 20px;
}
</style>
