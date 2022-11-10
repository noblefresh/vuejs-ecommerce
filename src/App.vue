<script setup>
import { RouterLink, RouterView } from 'vue-router'
import PageHeader from './components/PageHeader.vue'

</script>

<template>
  <header>
    <page-header :productId="products" />
  </header>
  
  <RouterView @addp="addP($event)" />
  <div class="fixed top-12 bg-green-600 text-white z-50 border text-md uppercase shadow-lg py-1 px-4 rounded-lg transistion-all duration-700" :class="notify">item added successfully</div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      products:[],
      notify:'-right-64',
      cartId:'',
      product_variant_id:null
    }
  },
  mounted(){
    this.checkCartID()
  },
  methods:{

      getCartID(){
        axios.post(`${import.meta.env.VITE_baseUrl}/store/carts`).then((res) => {
        localStorage.cart_id = res.data.cart.id;
      });
    },

    checkCartID(){
      this.cartId = localStorage.cart_id;
      if (!this.cartId) {
        this.getCartID();
      }
    },
    
    addP(data){
        this.cartId = localStorage.cart_id;
        axios.post(`${import.meta.env.VITE_baseUrl}/store/carts/${this.cartId}/line-items`, {
          variant_id: data,
          quantity: 1,
        })
        .then(({ data }) => {
            this.products.push(data)
            localStorage.cart = this.products
            this.notify = 'right-3'
            var inter = setInterval(() =>{
              this.notify='-right-64'
              clearInterval(inter)
            },1000)
        })
    }
  }
}
</script>