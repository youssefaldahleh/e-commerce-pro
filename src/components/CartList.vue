<template>
  <div class="contanier">
    <div class="header">
      <p class="boom">Boom >></p>
      <button class="close">X</button>
    </div>
    <p>Your Cart</p>
    <div class="carts">
      <div v-for="chosen in chosenPorduct" :key="chosen.id" class="cart">
        <P>{{ chosen.name }}</P>
        <input type="number" v-model="chosen.quantity" />
        <p>BRL {{ chosen.quantity * chosen.price }}.00</p>
        <ClearIcon @click="clear(chosen.id)"></ClearIcon>
      </div>
      <p class="total">Total Amount BRL {{ totalAmount }}.00</p>
    </div>
  </div>
</template>
<script>
import ClearIcon from "./ClearIcon.vue";
export default {
  data() {
    return {
      ProductList: this.chosenPorduct,
      totalAmount: null,
    };
  },
  components: {
    ClearIcon,
  },
  updated() {
    this.totalAmount = this.chosenPorduct.reduce(
      (acc, item) => acc + item.price * item.quantity
    );
  },
  created() {
    this.totalAmount = this.chosenPorduct.reduce(
      (acc, item) => acc + item.price,
      0
    );
  },

  methods: {
    clear(id) {
      // this.ProductList.pop(chosen);
      const productindex = this.ProductList.findIndex((prod) => prod.id === id);
      this.ProductList.splice(productindex, 1);
      console.log(this.chosenPorduct.length);
      console.log(this.ProductList);
    },
  },
};
</script>
<style scoped>
.contanier {
  background-color: #ddd;
  padding-bottom: 100px;
}
.cart {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1px solid #494545;
  border-radius: 12px;
  padding: 10px;
  margin-bottom: 10px;
}
.cart p {
  width: 200px;
}
.carts {
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.26);
  border-radius: 12px;
  margin: auto;
  padding: 10px;
  width: 80%;
}
.total {
  font-weight: bold;
  margin-left: 350px;
  margin-top: 20px;
}
.close {
  border: none;
  background-color: transparent;
  color: #494545;
  cursor: pointer;
}
.header {
  display: flex;
  justify-content: space-between;
}
.boom {
  color: rgb(219, 200, 27);
  font-weight: bold;
}
</style>
