<template>
    <div>
        <div class="py-28">
            <div class="max-w-6xl mx-auto py-4 space-y-5">
                <div class="flex">
                    <div class="flex-grow text-4xl font-extrabold">Special Qualities For You</div>
                </div>
                <div class="grid gap-20 grid-cols-1 md:grid-cols-2 lg:grid-cols-3 px-3">
                    <div v-for="(products, i) in fetchData" :key="i" class="rounded-lg shadow-xl" style="">
                        <router-link :to="{ name: 'single-product', params: { id: products.id }}">
                        <div class=" bg-white w-full flex justify-center items-center">
                            <img :src="products.thumbnail" alt="" srcset="">
                        </div>
                        <div class="bg-purple-100 py-8 relative font-bold text-xl w-full flex flex-col justify-center px-6">
                            <div class="">{{ products.title}}</div>
                            <div class="">
                                &euro; {{ products.variants[0].prices[0].amount }}
                            </div>
                        </div>
                        </router-link>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import { RouterLink } from 'vue-router';

export default ({
    data(){
        return{
            fetchData:[]
        }
    },
    mounted(){
        // calling the fetchProducts method when the page has loaded
        this.fetchProducts();
    },
    methods:{
        fetchProducts(){
            axios.get(`${import.meta.env.VITE_baseUrl}/store/products`)
            .then((data) => {
                    this.fetchData = data.data.products
                }).catch(err => console.log(err.products));
        }
    }
})
</script>