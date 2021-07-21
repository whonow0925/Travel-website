<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" /> -->
    <draw-board></draw-board>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
// import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src
import DrawBoard from "@/components/drawBoard/DrawingBoard.vue";

export default Vue.extend({
  name: "Home",
  components: {
    // HelloWorld,
    DrawBoard,
  },
});
</script>
