<template>
  <div
    class="relative border border-red-600 rounded-xl shadow-lg w-72 h-auto mt-4 p-4 flex flex-col justify-center items-center">
    <img
      class="rounded-xl object-cover h-[256px] w-full"
      :src="getFullImageUrl(imageUrl)"
      alt=""/>

      <!-- edit menu button for admin -->
      <a v-if="edit_menu != null && auth.getUser.role === 'chef'" :href="edit_menu"
      class="absolute top-2 right-2 ease-out duration-200 hover:-translate-y-1 hover:translate-x-1 shadow-lg hover:bg-red-500 bg-red-600 text-white px-2 py-1 rounded-xl">
        <i class="bi bi-pencil-square"></i>
        แก้ไข
      </a>
      <!-- end -->
      
    <div class="flex flex-col mt-4 justify-center items-center w-full">
      <p class="mt-2 text-2xl">
        <slot name="title"> Default title </slot>
      </p>
      <p class="mt-2 text-xl font-light">
        ฿
        <slot name="price"> Default price </slot>
      </p>

      <NuxtLink v-if="auth.getUser.role !== 'admin'" :to="to" class="mt-4 w-full">
        <Button class="w-full">
          <i class="bi bi-plus-lg mr-1"></i>
          <slot name="button"> Defaut button text </slot>
        </Button>
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
const auth = useAuthStore()
defineProps({
  imageUrl: String,
  edit_menu: String,
  to: String
})

const getFullImageUrl = (imageUrl) => {
  // Combine the base path with the image URL
  return `/_nuxt/public/images/chef_menus/${imageUrl}`;
};
</script>
