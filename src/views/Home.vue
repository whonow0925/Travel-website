<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
    <clock></clock>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
// import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import Clock from "@/components/clock/Clock.vue";

export default Vue.extend({
  name: "Home",
  components: {
    // HelloWorld,
    Clock,
  },
});
</script>
