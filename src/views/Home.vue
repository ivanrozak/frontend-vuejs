<template>
  <div class="home">
    <Mainheader />
    <b-container class="centered">
      <img alt="Vue logo" src="../assets/logo.png" />

      <Navbar />
      <b-card>
        <h5>Interpolation</h5>
        <p>My name is {{ name }}</p>
      </b-card>
      <b-card>
        <h5>Computed</h5>
        <p>Original Message : {{ message }}</p>
        <p>Reverse message : {{ reverseMessage }}</p>
      </b-card>
      <b-card>
        <h5>Directive</h5>
        <hr />
        <h6>v-if</h6>
        <div v-if="rule === 1">Kamu adalah Admin</div>
        <div v-else-if="rule === 2">Kamu adalah user</div>
        <div v-else>Kamu adalah Customer</div>
        <h6>v-show</h6>
        <div v-show="rule === 3">Kamu bukan siapa siapa</div>
        <hr />
        <h6>v-for</h6>
        <ul>
          <li v-for="(item, index) in dataProduct" :key="index">
            {{ index }} - {{ item }}
            <h5>{{ item.product_name }}</h5>
            <p>{{ item.product_price }}</p>
          </li>
        </ul>
        <h6>v-on</h6>
        <!-- v-on:click = @click -->
        <button v-on:click="boom()">Click Me!</button>
        <!-- v-model untuk menambahkan hint pada input -->
        <!-- sifat reload di v-on bisa dihandel dg menambahkan .prevent setelah click -->
        <input type="text" v-model="searchData" v-on:keyup.enter="search()" />
        <h6>v-bind</h6>
        <!-- fungsinya untuk memanggil data -->
        <a v-bind:href="rule === 1 ? urlGoogle : urlYoutube">Click link href</a>
      </b-card>
      <b-card>
        <h5>Component Communication</h5>
        <!-- <FormInput v-bind:dataProductName="product_name" /> -->
        <FormInput
          :dataProductName="product_name"
          @changeProductName="product_name = $event"
        />
        <br />
        <label>{{ product_name }}</label>
      </b-card>
    </b-container>
  </div>
</template>

<script>
// [1] step pertama import komponen
import Navbar from '../components/_base/Navbar'
import Mainheader from '../components/_base/Mainheader'
import FormInput from '../components/_base/FormInput'

export default {
  name: 'Home',
  // [2] step 2 mendaftarkan komponen yang sudah kita import
  components: {
    Navbar,
    Mainheader,
    FormInput
  },
  data() {
    return {
      name: 'Ivan Rozak',
      message: 'Hello World',
      rule: 1,
      searchData: 'Sepatu Baru',
      dataProduct: [
        {
          product_name: 'Meja',
          product_price: '50000'
        },
        {
          product_name: 'Kursi',
          product_price: '30000'
        }
      ],
      urlGoogle: 'http://google.com',
      urlYoutube: 'http://youtube.com',
      product_name: 'Sepatu Baru'
    }
  },
  computed: {
    reverseMessage: function() {
      return this.message
        .split(' ')
        .reverse()
        .join(' ')
    }
  },
  methods: {
    boom() {
      console.log('Boom !')
      alert('Boom !')
    },
    search() {
      console.log('Process Search !')
      console.log(this.searchData)
    },
    //ini cara ke 2
    changeNameProduct(event) {
      this.product_name = event
    }
  }
}
</script>

<style scoped>
.centered {
  text-align: center;
}
</style>
