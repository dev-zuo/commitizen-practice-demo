<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png" />
    <p>fix type commit test</p>
    <p>fix type commit test 2rd</p>
    <p>feat type commit test</p>
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import HelloWorld from "@/components/HelloWorld.vue"; // @ is an alias to /src

export default defineComponent({
  name: "Home",
  components: {
    HelloWorld,
  },
});
</script>
