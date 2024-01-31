<template>
  <div
    v-if="show"
    class="w-full h-screen fixed inset-0 z-50 bg-gray-800 bg-opacity-50 shadow-lg shadow-gray-600 items-center h-fit pt-20"
  >
    <div class="gap-1 bg-white w-1/2 rounded-lg m-auto rounded-lg p-10">
      <h1 class="font-bold text-xl text-center mb-4">Update Product</h1>
      <div @submit.prevent="updateproduct">
        <div class="grid grid-cols-2 w-full h-full">
          <div class="w-4/5 my-2 flex flex-col gap-3 items-start">
            <label class="" for="Sname">Product Code</label>
            <input
              v-model="pcode"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="sname"
              type="text"
              required
            />
          </div>
          <div class="w-4/5 my-2 flex flex-col gap-3 items-start">
            <label class="" for="Sname">Product Name</label>
            <input
              v-model="productName"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="sname"
              type="text"
              required
            />
          </div>
          <div class="w-4/5 my-2 flex flex-col gap-3 items-start">
            <label for="total">Catagory</label>
            <input
              v-model="category"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="total"
              type="text"
              required
            />
          </div>
          <div class="w-4/5 my-2 flex flex-col items-start gap-3">
            <label for="minimum">Price</label>
            <input
              v-model="price"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="minimim"
              type="number"
              required
            />
          </div>
          <div class="w-4/5 my-2 flex flex-col items-start gap-3">
            <label for="amount">Quantity</label>
            <input
              v-model="quantity"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="amount"
              type="number"
              required
            />
          </div>
          <div class="w-4/5 my-2 flex flex-col items-start gap-3">
            <label for="maximum">Supliyer</label>
            <input
              v-model="supplier"
              class="p-2 w-full rounded-lg border-none bg-blue-100"
              id="maximum"
              type="text"
              required
            />
          </div>
        </div>

        <div class="w-full flex justify-between pr-12 pt-4">
          <button
            class="self-start py-3 px-8 rounded-xl bg-gray-800 text-white"
            @click="$emit('toggleshowup')"
          >
            cancle
          </button>
          <button
            class="ml-12 self-end py-3 px-8 rounded-xl bg-[#d3af35]"
            type="submit"
            @click="updateproduct"
          >
            Save
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import axios from "axios";

const props = defineProps({
  show: {
    type: Boolean,
    required: true,
  },
  product: {
    type: Object,
  },
});

const pcode = ref(props.product?.pcode);
const productName = ref(props.product?.productName);
const category = ref(props.product?.category);
const price = ref(props.product?.price);
const quantity = ref(props.product?.quantity);
const supplier = ref(props.product?.supplier);

const updateproduct = async () => {
  const data = {
    pcode: pcode.value,
    category: category.value,
    supplier: supplier.value,
    price: price.value,
    productName: productName.value,
    quantity: quantity.value,
  };
  const token = localStorage.getItem("token");
  await axios
    .put(`http://10.4.192.40:8001/api/Product/${props.product.id}`, data, {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    })
    .then((res) => {
      console.log(res);
      window.location.reload()
    })
    .catch((err) => {
      console.log(err);
    });
};
</script>

<style lang="scss" scoped></style>
