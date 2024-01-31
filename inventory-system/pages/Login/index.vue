<template>
  <div class="w-full mt-28">
    <!-- <Navebar :title="title" :links="links" /> -->
    <form @submit.prevent="handleLogin"
      class="flex flex-col gap-1 bg-white shadow-lg shadow-gray-300 m-auto items-center justify-center w-1/2 h-1/2 rounded-lg p-10"
    >
    <!-- <img src="@/asssets/images/blackTextLogo.png" class="w-10 self-start" /> -->
      <h1 class="font-bold">LOG_IN</h1>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <label class="" for="email">Emial</label>
        <input
          class="p-2 w-3/4 rounded-lg border-none bg-blue-100"
          id="email"
          type="email"
          required
          v-model="email"
        />
      </div>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <label for="password">Password</label>
        <input
          class="p-2 w-3/4 rounded-lg border-none bg-blue-100"
          id="password"
          type="password"
          v-model="password"
          required
        />
      </div>
      <p class="text-red-400 font-sm">{{errmessage}}</p>
      <div class="w-3/4 my-2 flex flex-col gap-3 items-start">
        <button
          class=" w-3/4 py-3 px-8 rounded-xl bg-[#d3af35] "
          type="submit"
        >
       Login
        </button>
        <p>have no account <NuxtLink to="/">Sign-up</NuxtLink></p>
      </div>
      
    </form>
  </div>
</template>

<script setup>
import axios from 'axios'
const email = ref("");
const password = ref("");
const errmessage = ref("");

const handleLogin = async () => {
  const data = {
    email: email.value,
    password: password.value,
  };
  await axios
    .post("http://10.4.192.43:8001/api/Accounts/Login", data)
    .then((res) => {
      console.log(res);

      // localStorage.setItem("token", res.data.token);
      router.push({ path: "/product" });
    })
    .catch((err) => {
      console.log(err);
      // errmessage.value = err.response.data.message;
    });
};
</script>

<style lang="scss" scoped></style>
