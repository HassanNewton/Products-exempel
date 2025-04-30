<template>
  <div></div>
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
    async,
  },
  mounted() {
    this.fetchProducts();
  },
};
</script>
