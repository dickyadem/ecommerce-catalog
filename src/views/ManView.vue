<template>
  <div class="product">
    <img :src="product.img" class="product-image" />
    <h2 class="product-title">{{ product.h2 }}</h2>
    <p class="product-description">{{ product.p }}</p>
    <div class="product-price">{{ product.price }}</div>
    <button class="buy-btn" @click="buyProduct">Buy</button>
    <button class="next-btn" @click="nextProduct">Next</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      product: {
        img: '',
        h2: '',
        p: '',
        price: '',
      },
      index: 1,
      gender: 'men',
      availableProducts: {
        men: [1, 2, 3, 4],
        women: [5, 7, 8, 10, 19, 18, 17, 16, 15],
      },
      currentIndex: 0,
    };
  },
  mounted() {
    this.getProduct();
  },
  methods: {
    async getProduct() {
      const response = await fetch(
        `https://fakestoreapi.com/products/${
          this.availableProducts[this.gender][this.currentIndex]
        }`
      );
      const data = await response.json();

      this.product.img = data.image;
      this.product.h2 = data.title;
      this.product.p = data.description;
      this.product.price = `$${data.price}`;
    },
    buyProduct() {
      alert('Product bought!');
    },
    nextProduct() {
      this.currentIndex =
        (this.currentIndex + 1) % this.availableProducts[this.gender].length;
      this.getProduct();
    },
  },
  watch: {
    gender() {
      this.currentIndex = 0;
      this.getProduct();
    },
  },
  computed: {
    isUnavailable() {
      return (
        !this.availableProducts[this.gender] ||
        this.availableProducts[this.gender].length === 0
      );
    },
  },
};
</script>
<style>
.product-container {
  max-width: 800px;
  margin: 0 auto;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
}

.product {
  margin: 20px;
  padding: 20px;
  text-align: center;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
}

.product-image {
  width: 200px;
  height: 200px;
  object-fit: contain;
  margin-bottom: 10px;
}

.product-title {
  font-size: 24px;
  font-weight: bold;
  margin-bottom: 10px;
}

.product-description {
  font-size: 16px;
  margin-bottom: 10px;
}

.product-price {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 20px;
}

.buy-btn {
  padding: 10px 20px;
  border: none;
  background-color: #0077b6;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
}

.buy-btn:hover {
  background-color: #023e8a;
}

.next-btn {
  padding: 10px 20px;
  border: none;
  background-color: #0077b6;
  color: #fff;
  font-size: 16px;
  cursor: pointer;
  margin-top: 20px;
}

.next-btn:hover {
  background-color: #023e8a;
}

.unavailable-product {
  text-align: center;
  font-size: 24px;
  font-weight: bold;
  margin: 20px;
}
</style>