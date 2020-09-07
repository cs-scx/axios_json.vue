<template>
  <div id="app" class="container">
    <h1>{{ overview.name }}</h1>
    <img width="300px" src id="img0" />
    <hr />
    <h3>
      <span class="badge badge-secondary badg">简介：</span>
      <span class="after">
        <hr />
      </span>
    </h3>
    <div class="text">
      <p>{{overview.description}}</p>
    </div>
    <table class="table table-hover">
      <tbody>
        <tr>
          <td v-for="(item, index) in catalogue" :key="index">
            <a href>{{ item }}</a>
          </td>
        </tr>
      </tbody>
    </table>
    <h3>
      <span class="badge badge-secondary badg">成分：</span>
      <span class="after">
        <hr />
      </span>
    </h3>
    <div class="text">
      <p>{{ ingredient }}</p>
    </div>
    <h3>
      <span class="badge badge-secondary badg">化学结构式：</span>
      <span class="after">
        <hr />
      </span>
    </h3>
    <img width="300px" src alt id="img1" />
    <h3>
      <span class="badge badge-secondary badg">性状：</span>
      <span class="after">
        <hr />
      </span>
    </h3>
    <div class="text">
      <p>{{ feature }}</p>
    </div>
    <h3>
      <span class="badge badge-secondary badg">适应症：</span>
      <span class="after">
        <hr />
      </span>
    </h3>
    <div class="text">
      <p>{{ adapt_symptom }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
const baseURL = "http://localhost:3000/content"; //json resource

export default {
  name: "App",
  data() {
    return {
      overview: "",
      catalogue: "",
      ingredient: "", //成分
      imgs: [],
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
      this.imgs = this.overview.data;
      this.feature = this.overview.data[1].feature;
      this.adapt_symptom = this.overview.data[2].adapt_symptom;
      document.getElementById("img0").src = this.overview.img;
      document.getElementById("img1").src = this.imgs[0].imgUrl;
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
  color: #2c3e50;
  margin-top: 60px;
}
.text {
  background-color: rgba(62, 85, 134, 0.2);
  margin-left: 1.5em;
  border-radius: 54px;
  box-shadow: 3px 2px 5px #ccd0d3;
}
.text p {
  padding: 15px 20px;
  letter-spacing: 3px;
  text-indent: 40px;
}
.after > hr {
  width: 80%;
  background-color: #2c3e50;
  height: 3px;
  position: relative;
  top: -35px;
  left: -35px;
  border: none;
  z-index: -1;
}
.badg {
  background-color: #2c3e50;
}
h3 > span:first-child {
  border-radius: 20px;
  padding: 8px 16px;
}
h1 {
  font-weight: 700;
  letter-spacing: 5px;
  text-shadow: 2px 3px 2px rgba(105, 121, 161, 0.4);
}
</style>
