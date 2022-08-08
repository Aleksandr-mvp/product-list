<template>
  <div v-if="products.length" style="display: flex; flex-wrap: wrap; width:1200px">
    <div v-for="product in products" :key="product.title" class="card">
      <div>
        <img class="img" :src="product.imageUrl" alt="img">
      </div>
      <div class="content">
        <h2 class="tile_content">{{ product.title }}</h2>
        <p class="text_content">
          {{ product.description }}
        </p>
        <span class="price">
          {{ product.price.replace(/(\d)(?=(\d{3})+([^\d]|$))/g, '$1 ') }}
        </span>
        <div style="display: flex; justify-content: end">
          <div @click="deleteProduct(product)" class="remove">✖</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "ContentProduct",
  props: ['products'],
  methods: {
    deleteProduct(product) {
      this.products = this.products.filter(item => item !== product)
    },
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}
.card {
  margin-left: 10px;
  width: 332px;
  height: 423px;
  left: 380px;
  top: 83px;

  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.img {
  width: 332px;
  height: 200px;
  left: 380px;
  top: 83px;
  border-radius: 4px 4px 0px 0px;
}

.content {
  left: 380px;
  top: 83px;
  padding: 16px;

  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.tile_content {
  height: 25px;
  left: 396px;
  top: 299px;

  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 20px;
  line-height: 25px;

  color: #3F3F3F;
}

.text_content {
  word-break: break-all;
  width: 300px;
  height: 80px;
  left: 396px;
  top: 340px;

  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 16px;
  line-height: 20px;

  color: #3F3F3F;
}

.price {
  width: 117px;
  height: 30px;
  left: 396px;
  top: 452px;

  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 24px;
  line-height: 30px;

  color: #3F3F3F;
}

.remove {
  cursor: pointer;
  margin-left: 5px;
  text-align: center;
  width: 32px;
  height: 32px;
  left: 1036px;
  top: 75px;

  background: #FF8484;
  box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}
</style>
