<template>
  <div
    class="bg-white px-5 fixed top-0 left-0 right-0 w-full h-16 flex justify-between items-center shadow-sm shadow-gray-400 z-50"
  >
    <div class="flex gap-4 items-center">
      <div >
        <Icon icon="material-symbols:menu" width="30" />
      </div>
      <!-- <img src="@/asssets/images/blacktextlogo.png" class="w-10" /> -->
    </div>
    <NuxtLink >
      <div>
        <p> links === "/" ? "Home" : links </p>
      </div>
    </NuxtLink>
    <div class="flex gap-4">
      <div>
        <p> data?.name</p>
        <p> data?.email </p>
      </div>
    </div>
  </div>
</template>

<script setup>

</script>

<style lang="scss" scoped></style>
