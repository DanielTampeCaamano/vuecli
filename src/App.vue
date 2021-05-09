<template>
  <div class="container">
    <div class="row">
      <div class="col-md-12">
        <h1>Productos</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-md-12">
        <product-form @add-product="addProduct"></product-form>
        <product-table
          :products="products"
          @delete-product="deleteProduct"
          @update-product="updateProduct"
        ></product-table>
      </div>
    </div>
  </div>
</template>

<script>
import ProductTable from "@/components/ProductTable.vue";
import ProductForm from "@/components/ProductForm.vue";
export default {
  name: "App",
  components: {
    ProductTable,
    ProductForm,
  },
  data() {
    return {
      products: [
        {
          nombre: "Uranio",
          descripcion: "Para uso casero",
          precio: 500,
        },
        {
          nombre: "Unicornio",
          descripcion: "3 cuernos",
          precio: 600,
        },
        {
          nombre: "Dinosaurio",
          descripcion: "Velociraptor 5 metros",
          precio: 340,
        },
      ],
    };
  },
  methods: {
    addProduct(product) {
      this.products = [...this.products, product];
    },
    deleteProduct(index) {
      this.products.splice(index, 1);
    },
    updateProduct(editIndex, editProduct) {
      this.products = this.products.map((product, index) =>
        index === editIndex ? editProduct : product
      );
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
