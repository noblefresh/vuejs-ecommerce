<script setup>
import PageHeader from '../components/PageHeader.vue'
import Products from '../components/Products.vue'
import FooterComponent from '../components/FooterComponent.vue'
</script>

<template>
  <main>
    <div class="bg-purple-300 w-full">
      <div class="" style="height: 92vh">
          <div class="max-w-6xl mx-auto h-full flex items-center">
              <div class="grid gap-1 px-3 grid-cols-1 mt-8 md:grid-cols-5">
                  <div class="md:col-span-2 order-2 flex flex-col justify-center space-y-12">
                      <div class="space-y-5">
                          <div class="font-extrabold w-full text-6xl">
                              Nothing But Qualities
                          </div>
                          <div class="text-lg leading-7 max-w-md">
                              We sell quality Hoddies, Joggers, Shorts and lot more
                          </div>
                      </div>
                      <div>
                        <router-link :to="{ name: 'products'}">
                          <span class='w-fit  cursor-pointer transistion-all duration-300 hover:text-purple-400 text-white px-3  py-3 bg-gradient-to-r from-purple-500 to-pink-500 rounded flex justify-center items-center'>
                                Explore More
                          </span>
                        </router-link>
                      </div>
                  </div>
                  <div class="md:col-span-3 flex justify-center md:order-2">
                      <img src="/src/images/hoddie.png" class="bottom-1 relative h-11/12" style="">
                  </div>
              </div>
          </div>
      </div>
      <div class="flex justify-center bg-purple-300 py-4 pb-10 w-full">
          <div class="h-14 rounded-2xl relative" style="border: 1px solid black;padding:3px 6px 3px">
              <div class="bg-black rounded-full relative top-10" style="padding: 3px"></div>
          </div>
      </div>
    </div>

    <products/>

    <footer-component/>
  </main>
</template>