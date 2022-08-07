<template>
  <div style="display: flex" class="container">
    <div>
      <form style="padding: 24px" @submit.prevent="addProduct()">
        <div style="margin-bottom: 10px">
          <label>
            <span class="title_form">Наименование товара<span style="color: red">*</span></span>
          </label>
          <div>
            <input
              v-model="$v.form.title.$model"
              :disabled="disabled"
              type="text"
              class="ipt"
              autocomplete="off"
              placeholder="Введите наименование товара"
              :class="{'is-invalid': $v.form.title.$dirty && titleErrors.length > 0}"
            >
          </div>
          <div
            v-for="error in titleErrors"
            :key="error"
            class="invalid-form"
          >
            {{ error }}
          </div>
        </div>

        <div style="margin-bottom: 10px">
          <label>
            <span class="title_form">Описание товара</span>
          </label>
          <div>
            <textarea
              v-model="form.description"
              :disabled="disabled"
              class="txt"
              placeholder="Введите описание товара"
            >
            </textarea>
          </div>
        </div>

        <div style="margin-bottom: 10px">
          <label>
            <span class="title_form">Ссылка на изображение товара<span style="color: red">*</span></span>
          </label>
          <div>
            <input
              v-model="$v.form.imageUrl.$model"
              :disabled="disabled"
              type="text"
              class="ipt"
              autocomplete="off"
              placeholder="Введите ссылку"
              :class="{'is-invalid': $v.form.imageUrl.$dirty && imageUrlErrors.length > 0}"
            >
          </div>
          <div
            v-for="error in imageUrlErrors"
            :key="error"
            class="invalid-form"
          >
            {{ error }}
          </div>
        </div>

        <div style="margin-bottom: 15px">
          <label>
            <span class="title_form">Цена товара<span style="color: red">*</span></span>
          </label>
          <div>
            <input
              v-model="$v.form.price.$model"
              :disabled="disabled"
              type="text"
              class="ipt"
              placeholder="Введите цену"
              :class="{'is-invalid': $v.form.price.$dirty && priceErrors.length > 0}"
            >
          </div>
          <div
            v-for="error in priceErrors"
            :key="error"
            class="invalid-form"
          >
            {{ error }}
          </div>
        </div>

        <div>
          <button
            :disabled="checkForm()"
            type="submit"
            class="btn"
            :class="{'btnColor': !checkForm()}"
          >
            Добавить товар
          </button>
        </div>
      </form>
      <div>
        <input v-model="searchQuery"class="ipt" type="text" placeholder="Поиск по наименованию"/>
      </div>
    </div>
    <div>
      <ContentProduct :products="searchedProducts"/>
    </div>
  </div>
</template>

<script>
import {validationMixin} from "vuelidate";
import {required} from "vuelidate/lib/validators";
import ContentProduct from "~/components/products/ContentProduct";

export default {
  name: "FormsProduct",
  components: {ContentProduct},
  mixins: [validationMixin],
  data: () => ({
    form: {
      title: '',
      description: '',
      imageUrl: '',
      price: ''
    },
    searchQuery: '',
    products: [],
    disabled: false
  }),
  computed: {
    searchedProducts() {
      return this.products.filter(product => product.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    },
    titleErrors() {
      const errors = []
      if (!this.$v.form.title.required) errors.push('Поле является обязательным')
      return errors
    },
    imageUrlErrors() {
      const errors = []
      if (!this.$v.form.imageUrl.required) errors.push('Поле является обязательным')
      return errors
    },
    priceErrors() {
      const errors = []
      if (!this.$v.form.price.required) errors.push('Поле является обязательным')
      return errors
    },

  },
  methods: {
    addProduct() {
      const newProduct = {
        title: this.form.title,
        description: this.form.description,
        imageUrl: this.form.imageUrl,
        price: this.form.price,
      }
      this.products.push(newProduct)

      this.form.title = ''
      this.form.description = ''
      this.form.imageUrl = ''
      this.form.price = ''
    },
    checkForm() {
      return this.$v.$invalid
    },
  },
  mounted() {
    console.log(this.searchedProducts)
  },
  validations: {
    form: {
      title: {
        required
      },
      imageUrl: {
        required
      },
      price: {
        required
      }
    },
  }
}
</script>

<style scoped>
.container {
  position: absolute;
  width: 332px;
  height: 440px;
  left: 32px;
  top: 83px;

  background: #FFFEFB;
  box-shadow: 0px 20px 30px rgba(0, 0, 0, 0.04), 0px 6px 10px rgba(0, 0, 0, 0.02);
  border-radius: 4px;
}

.title_form {
  width: 95px;
  height: 13px;
  left: 56px;
  top: 107px;

  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  font-weight: 400;
  font-size: 12px;
  line-height: 13px;
  /* identical to box height */

  letter-spacing: -0.02em;

  /* Temp / Darks / Lesser */

  color: #49485E;
}

.ipt {
  border: none;
  text-indent: 5px;
  width: 284px;
  height: 36px;
  left: 56px;
  top: 124px;
  margin-top: 5px;

  /* Darks & Whites / White */

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.txt {
  border: none;
  text-indent: 5px;
  width: 284px;
  height: 108px;
  left: 56px;
  top: 193px;
  margin-top: 5px;

  /* Darks & Whites / White */

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.btn {
  cursor: pointer;
  width: 284px;
  height: 36px;
  left: 56px;
  top: 463px;

  background: #EEEEEE;
  border-radius: 10px;
  border: none;
}

.sort {
  width: 200px;
  height: 36px;
  left: 1287px;
  top: 31px;

  /* Darks & Whites / White */

  background: #FFFEFB;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  border-radius: 4px;
}

.select {
  -moz-appearance: none;
  -webkit-appearance: none;
  border: none;
  position: relative;
  outline: none;
  padding: 5px;
  padding-right: 100px;

  font-family: 'Source Sans Pro', sans-serif;
  font-style: normal;
  color: #928e8e;
}

select:after{
  content: "";
  display: block;
  width: 25px;
  height: 25px;
  background-image: url("/put_k_strelke");
  position: absolute;
  right: 5px;
  top: 5px;
}

.btnColor {
  background: linear-gradient(45deg, #13547a, #80d0c7);
  color: #EEEEEE;
}

.invalid-form {
  width: 100%;
  margin-top: 0.25rem;
  font-size: 85.71428571%;
  color: #d63939;
  font-family: 'Source Sans Pro', sans-serif;
}

.is-invalid {
  border-color: #d63939;
}
</style>
