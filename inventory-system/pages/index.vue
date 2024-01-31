<template>
  <div class="w-full mt-28">
    <div
      class="flex flex-col gap-1 bg-white shadow-lg shadow-gray-200 m-auto items-center w-1/2 h-fit rounded-lg p-10"
    >
      <h1 class="font-bold">Sign-up</h1>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <label class="" for="email">Emial</label>
        <input
          class="p-2 w-3/4 rounded-lg border-none"
          id="email"
          type="email"
          required
          v-model="email"
        />
      </div>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <label for="password">Password</label>
        <input
          class="p-2 w-3/4 rounded-lg border-none"
          id="password"
          type="password"
          v-model="password"
        />
      </div>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <label for="cpassword">Confirm Password</label>
        <input
          class="p-2 w-3/4 rounded-lg border-none"
          id="cpassword"
          type="password"
          v-model="cpassword"
        />
      </div>
      <button
        class="ml-12 self-end py-3 px-8 rounded-xl bg-[#d3af35]"
        @click="handleRegister"
      >
        Register
      </button>
      <p>Have acount <NuxtLink to="/login">Login</NuxtLink></p>
    </div>
  </div>
</template>

<script setup>
import axios from 'axios'
import {useRouter} from 'vue-router'

const router = useRouter();
const email = ref("");
const password = ref("");
const cpassword = ref("");
const errmessage = ref("");

const handleRegister = async () => {
  const data = {
    email: email.value,
    password: password.value,
    confirmPassword: cpassword.value,
  };
  await axios
    .post("http://10.4.192.40:8001/api/Accounts/Register", data)
    .then((res) => {
      console.log(res);
      router.push({ path: "/login" });
    })
    .catch((err) => {
      console.log(err.response.data.message);
      errmessage.value = err.response.data.message;
    });
};
</script>

<style lang="scss" scoped></style>
