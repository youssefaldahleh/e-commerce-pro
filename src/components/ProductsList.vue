<template>
  <div class="header">
    <p class="boom">Boom >></p>
    <div>
      <span class="conterspan">{{ this.chosenPorduct.length }}</span>
      <Carticon @click=""> </Carticon>
    </div>
  </div>
  <p class="">Products</p>
  <input
    class="search"
    type="text"
    v-model="search"
    placeholder="Search Product"
  />
  <div class="contanier">
    <div
      v-for="Product in filteredPorduct"
      :key="Product.id"
      class="productslist"
    >
      <div class="product">
        <img :src="Product.image" alt="" />
        <p class="product-name">{{ Product.name }}</p>
        <p class="productTitle">{{ Product.title }}</p>
        <p class="">JD {{ Product.price }}</p>
        <button @click="addPorduct(Product)" class="add">Add to Cart</button>
        <router-link to="/Cart"
          ><button @click="addPorduct(Product)" class="add">
            View Details
          </button></router-link
        >
      </div>
    </div>
  </div>
</template>
<style scoped>
.conterspan {
  margin-right: 5px;
}
.header {
  display: flex;
  justify-content: space-between;
}
.boom {
  color: rgb(219, 200, 27);
  font-weight: bold;
}
.search {
  min-width: 60%;
  margin: 20px 0;
  padding: 15px;
}
.search:focus {
  outline: none;
}
.contanier {
  display: grid;
  grid-template-columns: auto auto auto auto;
  row-gap: 20px;
  column-gap: 60px;
}

img {
  width: 100px;
  margin-top: 5px;
  min-height: 100px;
}
.product {
  border: 1px solid #ddd;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  border-radius: 12px;
  min-width: 250px;
  min-height: 350px;
}

.add {
  border-radius: 20px;
  border: none;
  padding: 10px;
  margin-bottom: 10px;
  cursor: pointer;
}
</style>
<script>
import Carticon from "./Carticon.vue";
export default {
  data() {
    return {
      Products: [],
      search: "",
    };
  },
  components: {
    Carticon,
  },
  methods: {
    addPorduct(product) {
      this.chosenPorduct.push(product);
      console.log(...this.chosenPorduct);
      console.log(this.chosenPorduct.length);
      product.quantity = 1;
    },
  },
  // fetch("https://run.mocky.io/v3/aace2a42-8ce2-4319-8cc5-8050f0a00513").then(

  created() {
    fetch("https://fakestoreapi.com/products").then((response) =>
      response.json().then((data) => {
        this.Products = data;
      })
    );
  },
  computed: {
    filteredPorduct: function () {
      return this.Products.filter((product) => {
        return product.title.match(this.search);
      });
    },
  },
};
</script>
