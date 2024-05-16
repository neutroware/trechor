<template>
  <div class="wrapper">
    <nav>
      <h1>Trechor</h1>
      <div id="search-container">
        <input type="search" v-model="searchInput" placeholder="Search product name here.." />
        <button @click="search">Search</button>
      </div>
    </nav>
    <div id="buttons">
      <button v-for="(category, index) in categories" :key="index"
        :class="{ 'button-value': true, active: selectedCategory === category }" @click="filterCategory(category)">
        {{ category }}
      </button>
    </div>
    <div id="products">
      <div v-for="(product, index) in products" :key="index">
        <div class="card" :class="[product.category, { hide: !matchesSearch(product) }]">
          <div class="image-container">
            <img :src=product.image />
          </div>
          <div class="container">
            <h5 class="product-name">{{ product.productName.toUpperCase() }}</h5>
            <h6>${{ product.price }}</h6>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import whiteTshirt from './assets/images/white-tshirt.jpg';
import shortSkirt from './assets/images/short-skirt.jpg';
import sportySmartwatch from './assets/images/sporty-smartwatch.jpg';
import knittedTop from './assets/images/knitted-top.jpg';
import blackLeatherJacket from './assets/images/black-leather-jacket.jpg';
import pinkTrousers from './assets/images/pink-trousers.jpg';
import brownJacket from './assets/images/brown-jacket.jpg';
import comfyGrayPants from './assets/images/comfy-gray-pants.jpg';

export default {
  data() {
    return {
      products: [
        {
          productName: "Regular White T-Shirt",
          category: "Topwear",
          price: "30",
          image: whiteTshirt,
        },
        {
          productName: "Beige Short Skirt",
          category: "Bottomwear",
          price: "49",
          image: shortSkirt,
        },
        {
          productName: "Sporty SmartWatch",
          category: "Watch",
          price: "99",
          image: sportySmartwatch,
        },
        {
          productName: "Basic Knitted Top",
          category: "Topwear",
          price: "29",
          image: knittedTop,
        },
        {
          productName: "Black Leather Jacket",
          category: "Jacket",
          price: "129",
          image: blackLeatherJacket,
        },
        {
          productName: "Stylish Pink Trousers",
          category: "Bottomwear",
          price: "89",
          image: pinkTrousers,
        },
        {
          productName: "Brown Men's Jacket",
          category: "Jacket",
          price: "189",
          image: brownJacket,
        },
        {
          productName: "Comfy Gray Pants",
          category: "Bottomwear",
          price: "49",
          image: comfyGrayPants,
        },
      ],
      selectedCategory: "all",
      searchInput: ""
    };
  },
  computed: {
    categories() {
      return ['all', ...new Set(this.products.map(product => product.category))];
    },
    products() {
      const products = this.products.filter(product => this.matchesSearch(product));
      return products
    }
  },
  methods: {
    filterCategory(category) {
      this.selectedCategory = category;
    },

    matchesSearch(product) {
      const sameCategory = this.selectedCategory === "all" ? true : product.category === this.selectedCategory

      if (this.searchInput) {
        return sameCategory && product.productName.toLowerCase().includes(this.searchInput.toLowerCase());
      } else {
        return sameCategory
      }
    }
  }
};
</script>