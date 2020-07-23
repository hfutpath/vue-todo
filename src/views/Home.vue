<template>
  <div class="home">
    Hey,Develop
    <TotalInfo v-bind:count="233" />
    <FundLists/>
  </div>
</template>

<script>
import TotalInfo from "~components/TotalInfo";
import FundLists from "~components/FundLists/index.vue"

export default {
  name: "Home",
  data() {
    return {};
  },
  components: { TotalInfo, FundLists },
 
};
</script>

<style scoped>
</style>
