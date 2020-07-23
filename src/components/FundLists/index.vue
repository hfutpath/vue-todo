<template>
  <div class="home">
    <p>
      <span>基金名称</span>
      <span>基金代码</span>
      <span>涨跌幅</span>
      <span>持有额</span>
      <span>估算收益</span>
      <span>持有份额</span>
      <span>排序</span>
      <span>特别关注</span>
      <span>删除</span>
    </p>
    <FundItem v-for="li in lists" v-bind="li" v-bind:key="li.fundcode" />
    <p>
      添加新基金：
      <input v-model="newFundCode" />
      <button @click="addFund">确定</button>
    </p>
  </div>
</template>


<script>
import FundItem from "./FundItem.vue";
import jsonp from "jsonp";
export default {
  name: "FundList",
  data() {
    return {
      newFundCode: "",
      lists: [],
    };
  },
  components: { FundItem },
  methods: {
    addFund() {
      jsonp(
        `http://fundgz.1234567.com.cn/js/${this.newFundCode}.js`,
        { name: "jsonpgz" },
        (err, response) => {
          console.log("response>>>>>>: ", response);
          this.lists.push(response);
          this.newFundCode = "";
        }
      );
    },
  },
};
</script>
