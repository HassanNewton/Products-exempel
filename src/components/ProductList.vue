<template>
  <div class="product-container">
    <h1>Produkt lista</h1>

    <form @submit.prevent="addProduct">
      <input v-model="newProduct.name" placeholder="Produkt namn" required />
      <input
        v-model.number="newProduct.price"
        type="number"
        placeholder="Produkt pris"
        required
      />
      <button type="submit">Lägg till produkt</button>
    </form>

    <ul class="product-list">
      <li v-for="product in products" :key="product.id">
        <div>
          <h2>{{ product.name }}</h2>
          <p>Pris: {{ product.price }} kr</p>
        </div>
        <button @click="deleteProduct(product.id)">Delete</button>
        <button @click="editProduct(product.id)">Edit</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [],
      newProduct: {
        name: "",
        price: 0,
      },
    };
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await fetch("http://localhost:3000/products");
        const data = await response.json();
        this.products = data;
        console.log("Products fetched successfully:", this.products);
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    },
    async addProduct() {
      try {
        const response = await fetch("http://localhost:3000/products", {
          method: "POST",
          headers: {
            "Content-Type": "application/json",
          },
          body: JSON.stringify(this.newProduct),
        });

        if (response.ok) {
          this.newProduct = {
            name: "",
            price: 0,
          };
          this.fetchProducts();
        }
      } catch (error) {
        console.error("Error adding product:", error);
      }
    },
    async deleteProduct(productId) {
      try {
        const response = await fetch(
          `http://localhost:3000/products/${productId}`,
          {
            method: "DELETE",
          }
        );

        if (response.ok) {
          this.fetchProducts();
        }
      } catch (error) {
        console.error("Error deleting product:", error);
      }
    },
  },
  mounted() {
    this.fetchProducts();
  },
};
</script>
