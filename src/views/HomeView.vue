<template>
  <div class="home">
    <div class="container mx-auto">
      <products />
    </div>
  </div>
</template>

<script>
import products from "../components/ProductsComp.vue";
export default {
  name: "HomeView",
  components: {
    products,
  },
};
</script>
