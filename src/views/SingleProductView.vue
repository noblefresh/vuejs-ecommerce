<script setup>
import FooterComponent from '../components/FooterComponent.vue'
</script>

<template>
    <main ref="addProd">
        <div class='py-20 px-4'>
            <div class='text-white max-w-6xl mx-auto py-2'>
                <div class='grid md:grid-cols-2 gap-20 grid-cols-1'>
                
                    <div class=''>
                        <div class="relative">
                            <img :src="imgArr[currentImg]" alt="no image" />
                            <div class="absolute overflow-x-scroll w-full bottom-0 right-0 p-4 flex flex-nowrap gap-4">
                                <div  v-for="(er,i) in imgArr.length" :key="i" class="flex w-full flex-nowrap gap-4 rounded-lg">
                                    <div @click="currentImg = i" :title="imgArr[i]" class="w-16 h-24 flex-none">
                                        <div class="h-full w-full rounded-lg cursor-pointer shadow-lg border overflow-hidden">
                                            <img :src="imgArr[i]" alt="" class="h-full w-full">
                                        </div>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>

                    <div class=''>
                        <div class='flex md:flex-col flex-col space-y-7 justify-center'>
                            <div class='text-black space-y-3'>
                                <h2 class='font-bold text-xl text-black'>{{product.title}}</h2>
                                <p class='text-sm'>{{product.description}}</p>
                            </div>

                            <div class='space-y-3'>
                            <div class='font-bold text-md text-black'>Select Size</div>
                            <div class='flex flex-row flex-wrap gap-4'>
                                <div v-for="(size,i) in sizes" :key="i" class="">
                                    <div @click="currentSize = size ; currentPrice = priceList[i]" :class="currentSize == size ? 'border-purple-300 bg-purple-100':'border-gray-100' " contenteditable="false" class='border-2 rounded-md cursor-pointer flex justify-center py-3 px-5'>
                                        <span class=' text-black text-sm'>{{size}}</span>
                                    </div>
                                </div>
                            </div>
                            </div>


                            <div>
                            <div class='flex flex-col space-y-3'>
                                <div>
                                <span class='text-gray-700 text-2xl font-san'>&euro; {{ currentPrice }}</span>
                                </div>

                                <div @click="addProduct(product)" class='bg-gray-900 cursor-pointer text-white w-full text-sm font-semibold py-3 flex justify-center cursor pointer hover:bg-white hover:border hover:border-gray-900 hover:text-black '>
                                    ADD TO CART
                                </div>
                            </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <footer-component/>
    </main>
</template>

<script>
import axios from 'axios'

export default {
    data(){
        return{
            currentImg : 0,
            imgArr:[],
            productData:[],
            product:[],
            productId:'',
            sizes:[],
            currentSize:'S',
            priceList:[],
            currentPrice: ''
        }
    },
    mounted(){
        this.productId = this.$route.params.id
        axios.get(`${import.meta.env.VITE_baseUrl}/store/products/${this.productId}`)
        .then((productData) => {
                this.product = productData.data.product;
                console.log(this.product);
                this.product.images.forEach(data => {
                    this.imgArr.push(data.url)                                    
                });
                this.currentPrice = this.product.variants[0].prices[0].amount
                this.product.variants.forEach(data => {
                    this.sizes.push(data.title)                    
                    this.priceList.push(data.prices[0].amount)                    
                });
            }).catch(err => console.log(err));
    },
    methods:{
        addProduct(product){
            this.$emit('addp',product)
        }
    }
}
</script>