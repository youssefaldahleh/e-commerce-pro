<template>
  <div class="home">
    <ProductsList></ProductsList>
  </div>
</template>

<script>
import ProductsList from "@/components/ProductsList.vue";

export default {
  name: "HomeView",
  components: {
    ProductsList,
  },
};
</script>
