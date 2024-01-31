import type { Product } from '#build/components'; import type { Product } from
'#build/components';
<template>
  <div
    class="w-4/5 text-left h-fit bg-white hover:shadow-xl hover:shadow-gray-300 border-2 hover:border-none text-black flex flex-col items-start pl-5 py-10 gap-5"
  >
    <div class="flex justify-between w-full pr-5">
      <h1><strong>Name:-</strong> {{ product?.productName }}</h1>
      <div v-if="show" @click="toggleshow">
        <strong>less</strong>
        <Icon icon="fe:arrow-down" width="30" height="30" />
      </div>
      <div v-if="!show" @click="toggleshow" class="flex gap-2 items-center">
        <strong>more</strong>
        <Icon icon="fe:arrow-up" width="30" height="30" />
      </div>
    </div>
    <div v-if="show" class="flex flex-col gap-2">
      <p><strong>Product code :-</strong> {{ product?.pcode }}</p>
      <p><strong>Product Name :-</strong>{{ product?.productName }}</p>
      <p><strong>Product Category :-</strong>{{ product?.category }}</p>
      <p><strong>Product Price:-</strong>{{ product?.price }}</p>
      <p><strong>Product Quantity:-</strong>{{ product?.quantity }}</p>
      <p><strong>Product Supplier:-</strong>{{ product?.supplier }}</p>
    </div>

    <div class="flex justify-between items-center pr-2 w-full">
      <button
        @click="deleteproduct"
        class="p-2 bg-[#d3af35] text-white rounded-lg cursor-pointer border-none"
      >
        Delete
      </button>
      <button
        class="p-2 bg-gray-800 text-white rounded-lg cursor-pointer border-none"
        @click="deleteproduct(Product?.id)"
      >
        Update
      </button>
    </div>
    <update :show="showup" @toggleshowup="toggleshowup" :product="product" />
  </div>
</template>

<script setup>
import { Icon } from "@iconify/vue";
const props = defineProps(["product"]);
const showup = ref(false);

const show = ref(false);
const toggleshow = () => {
  show.value = !show.value;
};

const toggleshowup = () => {
  showup.value = !showup.value;
};

const deleteproduct = async (id) => {
  const token = localStorage.getItem("token");
  await axios
    .delete(`http://10.4.114.206:8001/api/Product/${id}`, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    })
    .then((res) => {
      console.log(res);
    })
    .catch((err) => {
      console.log(err);
    });
};
</script>

<style lang="scss" scoped></style>
