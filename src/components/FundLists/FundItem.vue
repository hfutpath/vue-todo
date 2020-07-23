<template>
  <div class="home">
    <span>{{name}}</span>
    <span>{{fundcode}}</span>
    <input type="number" v-model="count" />
    <button v-on:click="$emit('remove')">删除</button>
  </div>
</template>

<script>
export default {
  name: "FundItem",
  props: {
    name: String,
    fundcode: String,
    gszzl: String,
  },
  data() {
    return {
      count: '',
    };
  },
};
</script>

