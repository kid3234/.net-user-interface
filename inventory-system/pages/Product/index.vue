<template>
    <div class="w-full h-full">
        <div>
          <Navbar  />
        </div>
        <div class="w-full h-40 pt-24 pr-10 text-right">
          <button
            @click="toggleshowadd"
            class="px-10 py-3 bg-[#d3af35] rounded-xl text-white"
          >
            Add Stock
          </button>
        </div>
        <addproduct :show="showadd" @toggleshowadd="toggleshowadd" />
        <div class="w-full h-full grid grid-cols-2 items-center gap-y-8 pl-60 pt-4">
          <product
            v-for="product in products"
            :key="product?.name"
            :product="product"
          />
        </div>
      </div>
</template>

<script setup>
import axios from 'axios'
const showadd = ref(false);
// const products= ref()
const products= [
    {pcode:"hhh33",productName:"kid",category:"ce22",price:120,quantity:12,supplier:"juea"},
    {pcode:"hhh33",productName:"kid",category:"ce22",price:120,quantity:12,supplier:"juea"},
    {pcode:"hhh33",productName:"kid",category:"ce22",price:120,quantity:12,supplier:"juea"},
    {pcode:"hhh33",productName:"kid",category:"ce22",price:120,quantity:12,supplier:"juea"}
    
]


const toggleshowadd = () => {
  showadd.value = !showadd.value;
};
onMounted(async ()=>{
    const token= localStorage.getItem('token')
    await axios.get("http://10.4.114.206:8001/api/Product",{
        headers: {
        Authorization: `Bearer ${token}`,
      },
    })
    .then(res=>{
        console.log(res);
        products.value= res.data
    }).catch(err=>{
        console.log(err);
    })
})

</script>

<style lang="scss" scoped>

</style>