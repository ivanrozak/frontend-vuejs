<template>
  <div class="product">
    <div class="centered">
      <img alt="Vue logo" src="../assets/logo.png" />
      <Navbar />
      <h1>This is Page Product</h1>
      <b-alert :show="alert">{{ isMsg }}</b-alert>
      <form>
        <input
          type="text"
          v-model="form.product_name"
          placeholder="Product Name ..."
        />
        <br />
        <input
          type="text"
          v-model="form.product_price"
          placeholder="Product Price ..."
        />
        <br />
        <input
          type="text"
          v-model="form.category_id"
          placeholder="Category Id ..."
        />
        <br />
        <input
          type="text"
          v-model="form.product_status"
          placeholder="Product Status ..."
        />
        <br />
        <button type="button" @click="postProduct()">Save</button>
        <button type="button" @click="patchProduct()">Update</button>
      </form>
      <hr />
      <b-container class="bv-example-row">
        <b-row>
          <b-col
            xl="3"
            lg="4"
            md="6"
            sm="12"
            v-for="(item, index) in products"
            :key="index"
          >
            <b-card
              v-bind:title="item.product_name"
              img-src="https://picsum.photos/600/300/?image=25"
              img-alt="Image"
              img-top
              tag="article"
              style="max-width: 20rem;"
              class="mb-2"
            >
              <b-card-text> Rp. {{ item.product_price }} </b-card-text>

              <b-button href="#" variant="primary">Add to Cart</b-button>
              <b-button href="#" variant="success" @click="setProduct(item)"
                >Update</b-button
              >
              <b-button variant="danger" @click="deleteProduct(item.product_id)"
                >Delete</b-button
              >
            </b-card>
          </b-col>
          <b-col xl="3" lg="4" md="6" sm="12">2 of 3</b-col>
          <b-col xl="3" lg="4" md="6" sm="12">3 of 3</b-col>
          <b-col xl="3" lg="4" md="6" sm="12">4 of 3</b-col>
        </b-row>
        <b-pagination
          v-model="currentPage"
          :total-rows="rows"
          :per-page="limit"
          @change="handlePageChange"
        ></b-pagination>
      </b-container>
    </div>
  </div>
</template>

<script>
// [1] step pertama import komponen
import Navbar from '../components/_base/Navbar'
import axios from 'axios'

export default {
  name: 'Product',
  // [2] step 2 mendaftarkan komponen yang sudah kita import
  components: {
    Navbar
  },
  computed: {
    rows() {
      return this.totalRows
    }
  },
  data() {
    return {
      products: [],
      form: {
        product_name: '',
        category_id: '',
        product_price: '',
        product_status: ''
      },
      alert: false,
      isMsg: '',
      product_id: '',
      currentPage: 1,
      totalRows: null,
      limit: 8,
      page: 1
    }
  },
  created() {
    this.getProduct()
  },
  methods: {
    getProduct() {
      axios
        .get(
          `http://localhost:3000/product?page=${this.page}&limit=${this.limit}`
        )
        .then(response => {
          console.log(response)
          this.totalRows = response.data.pagination.totalData
          this.products = response.data.data
        })
        .catch(error => {
          console.log(error)
        })
    },
    postProduct() {
      console.log(this.form)
      axios
        .post('http://localhost:3000/product', this.form)
        .then(response => {
          console.log(response)
          this.alert = true
          this.isMsg = response.data.msg
          this.getProduct()
        })
        .catch(error => {
          console.log(error)
        })
    },
    deleteProduct(product_id) {
      console.log(product_id)
    },
    setProduct(data) {
      console.log(data)
      // this.form = {
      //   product_name: 'data.product_name',
      //   category_id: 'data.category_id',
      //   product_price: 'data.product_price',
      //   product_status: 'data.product_status'
      // }
      this.form = data //cara simplenya
      this.product_id = data.product_id
    },
    patchProduct() {
      console.log(this.product_id)
      console.log(this.form)
    },
    handlePageChange(numberPage) {
      console.log(numberPage)
      this.page = numberPage
      this.getProduct()
    }
  }
}
</script>

<style scoped>
.centered {
  text-align: center;
}
</style>
