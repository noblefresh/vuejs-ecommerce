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
export default {
  setup() {
    const toast = useToast();
    return { toast }
  },
  data(){
    return{
      products:[],
      notify:'-right-64'
    }
  },
  methods:{
    addP(data){
      this.products.push(data)
      localStorage.cart = this.products
      this.notify = 'right-3'
      var inter = setInterval(() =>{
        this.notify='-right-64'
        clearInterval(inter)
      },1000)
    }
  }
}
</script>