<script setup>
import { ref, computed, onUpdated } from "vue"

/* Search input */
const searchQuery = ref("")

/* Sample product list */
const products = ref([
  "Laptop",
  "Phone",
  "Headphones",
  "Keyboard",
  "Mouse",
  "Monitor",
  "Printer",
  "Webcam",
  "Speaker",
])

/* Filtered products (reactive) */
const filteredProducts = computed(() => {
  return products.value.filter(product =>
    product.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

/* Reference to dropdown (DOM element) */
const dropdownRef = ref(null)

/* Runs AFTER every DOM update */
onUpdated(() => {
  console.log("Filtered products:", filteredProducts.value)

  if (dropdownRef.value) {
    console.log(
      "Dropdown height:",
      dropdownRef.value.offsetHeight + "px"
    )
  }
})
</script>

<template>
  <div class="search-container">
    <input
      type="text"
      v-model="searchQuery"
      placeholder="Search products..."
    />

    <ul v-if="searchQuery" ref="dropdownRef" class="dropdown">
      <li
        v-for="(product, index) in filteredProducts"
        :key="index"
      >
        {{ product }}
      </li>

      <li v-if="filteredProducts.length === 0">
        No results found
      </li>
    </ul>
  </div>
</template>

<style scoped>
.search-container {
  width: 300px;
  margin: 50px auto;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
}

.dropdown {
  border: 1px solid #ccc;
  margin-top: 5px;
  padding: 0;
  list-style: none;
  max-height: 150px;
  overflow-y: auto;
}

.dropdown li {
  padding: 8px;
  cursor: pointer;
}

.dropdown li:hover {
  background-color: #f0f0f0;
}
</style>
