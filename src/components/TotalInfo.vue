<template>
  <div class="total-info">
    <h1>这里是大盘的指数集合</h1>
    <ul>
      <li v-for="li in lists" :key="li.f12" :class="{up: li.f4 > 0}">
        <p>{{li.f14}}</p>
        <p></p>
        <p>{{li.f2}}</p>
        <p>
          <span>{{li.f4}}</span>
          <span>{{li.f3}}%</span>
        </p>
      </li>
    </ul>
  </div>
</template>
<script>

export default {
  name: "TotalInfo",
  data() {
    return {
      lists: [],
    };
  },
  props: {},
  created: function () {
    this.$axios
      .get(
        "https://push2.eastmoney.com/api/qt/ulist.np/get?fltt=2&fields=f2,f3,f4,f12,f14&secids=1.000001,1.000300,0.399001,0.399006"
      )
      .then((response) => {
        this.lists = response.data.data.diff;
      });
  },
};
</script>
<style>
ul {
  display: flex;
  justify-items: center;
}
li {
  display: inline-block !important;
  margin: 0 20px;
  color: green;
  text-align: center;
}
.up {
  color: red;
}
span + span {
    margin-left: 4px;
}
</style>