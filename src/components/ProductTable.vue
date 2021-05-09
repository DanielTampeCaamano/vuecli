<template>
  <div id="product-table">
    <table class="table">
      <div v-if="!products.length" class="alert alert-info" role="alert">
        No se han agregado productos
      </div>
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Descripción</th>
          <th>Precio</th>
          <th>Acciones</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(product, index) in products" :key="index">
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.nombre"
              type="text"
              class="form-control"
            />
          </td>
          <td v-else>{{ product.nombre }}</td>
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.descripcion"
              type="text"
              class="form-control"
            />
          </td>
          <td v-else>{{ product.descripcion }}</td>
          <td v-if="editIndex === index">
            <input
              v-model="editableProduct.precio"
              type="text"
              class="form-control"
            />
          </td>
          <td v-else>{{ product.precio }}</td>
          <td v-if="editIndex === index">
            <button class="btn btn-light me-2" @click="editIndex = -1">
              Cancelar
            </button>
            <button class="btn btn-success" @click="saveProduct()">
              Guardar
            </button>
          </td>
          <td v-else>
            <button
              class="btn btn-info me-2"
              @click="editProduct(product, index)"
            >
              Editar
            </button>
            <button
              class="btn btn-danger"
              @click="$emit('delete-product', index)"
            >
              Eliminar
            </button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>
<script>
export default {
  name: "product-table",
  props: {
    products: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      editableProduct: {},
      editIndex: -1,
    };
  },
  methods: {
    editProduct(product, index) {
      this.editableProduct = Object.assign({}, product);
      // this.editableProduct= {...product};
      this.editIndex = index;
    },
    saveProduct() {
      if (
        !this.editableProduct.nombre.length ||
        !this.editableProduct.descripcion.length ||
        this.editableProduct.precio < 1
      ) {
        return;
      }
      this.$emit("update-product", this.editIndex, this.editableProduct);
      this.editIndex = -1;
    },
  },
};
</script>