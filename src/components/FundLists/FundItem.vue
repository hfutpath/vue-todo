<template>
  <div class="home">
    <span>{{name}}</span>
    <span>{{fundcode}}</span>
    <span>{{gszzl}}</span>
    <span>{{count * (gsz || '').slice(-1)}}</span>
    <span>{{count * (gsz || '').slice(-1) * gszzl}}</span>
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
  data: () => ({
    count: "20",
  }),
};
</script>

