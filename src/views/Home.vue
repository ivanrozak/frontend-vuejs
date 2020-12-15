<template>
  <div class="home">
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
      </b-card>
    </b-container>
  </div>
</template>

<script>
// [1] step pertama import komponen
import Navbar from '../components/_base/Navbar'

export default {
  name: 'Home',
  // [2] step 2 mendaftarkan komponen yang sudah kita import
  components: {
    Navbar
  },
  data() {
    return {
      name: 'Bagus Tri Harjanto',
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
      urlYoutube: 'http://youtube.com'
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
    }
  }
}
</script>

<style scoped>
.centered {
  text-align: center;
}
</style>
