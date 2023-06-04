<template>
  <ProductDisplay />
</template>

<script>
import ProductDisplay from "@/components/ProductDisplay.vue";

export default {
  name: "App",
  components: {
    ProductDisplay,
  },
};
</script>

<style>
@import "@/assets/style/page.css";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
