<template>
<div>
  <div >
    <h2 class="page_title">Добавление товара</h2>
  </div>
  <div>
    <FormsProduct/>
  </div>
</div>
</template>

<script>
import FormsProduct from "~/components/products/FormsProduct";
import ContentProduct from "~/components/products/ContentProduct";
export default {
  name: "MainProducts",
  components: {FormsProduct, ContentProduct}

}
</script>

<style scoped>
.page_title {
  height: 35px;
  left: 32px;
  top: 32px;

  font-family: 'Source Sans Pro',sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 28px;
  line-height: 35px;

  color: #3F3F3F;
  margin-left: 25px;
}
</style>
