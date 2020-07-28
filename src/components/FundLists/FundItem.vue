<template>
  <p class="home">
    <span>{{name}}</span>
    <span>{{fundcode}}</span>
    <span>{{gszzl}}</span>
    <span>{{(count * gsz).toFixed(1)}}</span>
    <span>{{(count * gsz * gszzl).toFixed(1)}}</span>
    <span v-if="editing">
      <input type="number" v-model="count" />
    </span>
    <span v-else>{{count}}</span>
    <span v-if="editing">
      <button v-on:click="$emit('up')">▲</button>
    </span>
    <span v-if="editing">
      <button v-on:click="$emit('active', fundcode)" :class="{active: active}">✔</button>
    </span>
    <span v-if="editing">
      <button v-on:click="$emit('remove')">删除</button>
    </span>
    <span v-else>{{gztime}}</span>
  </p>
</template>

<script>
export default {
  name: "FundItem",
  props: {
    name: String,
    fundcode: String,
    gszzl: String,
    gsz: String,
    editing: Boolean,
    gztime: String,
    active: Boolean
  },
  data: () => ({
    count: "20",
  }),
};
</script>
<style>
.active {
  color: #3b99ff;
}
</style>

