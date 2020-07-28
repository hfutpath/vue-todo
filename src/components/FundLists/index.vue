<template>
  <div class="listContent">
    <p>
      <span v-for="title in titles">{{title}}</span>
    </p>
    <FundItem
      v-for="(li, index) in lists"
      v-bind="li"
      :key="li.fundcode"
      :active="active === li.fundcode"
      v-on:remove="lists.splice(index, 1)"
      v-on:active="setActive"
      v-on:up="setUp(index)"
      :editing="editing"
    />
    <button @click="toggleEditing">{{this.editing ? '完成编辑' :'编辑'}}</button>
    <p>
      添加新基金：
      <input v-model="newFundCode" @keyup.enter="addFund" />
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
      editing: false,
      active: "",
      titles: [
        "基金名称",
        "基金代码",
        "涨跌幅",
        "持有额",
        "估算收益",
        "持有份额",
        "更新时间",
      ],
    };
  },
  components: { FundItem },
  methods: {
    setUp(index) {
      if (index === 0) {
        return;
      }
      this.lists.splice(index - 1, 0, this.lists.splice(index, 1)[0]);
    },
    setActive(id) {
      this.active = id;
    },
    toggleEditing() {
      this.editing = !this.editing;
      this.titles = [
        "基金名称",
        "基金代码",
        "涨跌幅",
        "持有额",
        "估算收益",
        "持有份额",
      ].concat(this.editing ? ["排序", "特别关注", "删除"] : "更新时间");
    },
    addFund() {
      if (
        this.lists.some((item) => {
          return item.fundcode === this.newFundCode;
        })
      ) {
        return alert("该基金已存在于列表中");
      }
      jsonp(
        `http://fundgz.1234567.com.cn/js/${this.newFundCode}.js`,
        { name: "jsonpgz" },
        (err, response) => {
          console.log('err: ', err);
          this.lists.push(response);
          this.newFundCode = "";
        }
      );
    },
  },
};
</script>
<style>
.listContent p {
  display: flex;
  margin-bottom: 6px;
}
.listContent p input {
  width: 80%;
}
.listContent p span {
  display: inline-block;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  text-align: left;
}
.listContent p span:nth-child(1) {
  width: 20%;
}
.listContent p span:nth-child(2) {
  width: 8%;
}
.listContent p span:nth-child(3) {
  width: 8%;
}
.listContent p span:nth-child(4) {
  width: 8%;
}
.listContent p span:nth-child(5) {
  width: 8%;
}
.listContent p span:nth-child(6) {
  width: 8%;
}
.listContent p span:nth-child(7) {
  width: 8%;
}
.listContent p span:nth-child(8) {
  width: 8%;
}
.listContent p span:nth-child(9) {
  width: 8%;
}
</style>