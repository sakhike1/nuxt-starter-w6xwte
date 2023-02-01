<script setup lang="ts">
definePageMeta({
  middleware: ['auth'],
});
const user = useSupabaseUser();
onMounted(() => {
  watchEffect(() => {
    if (!user.value) {
      navigateTo('/login');
    }
  });
});
</script>
<template>
  <div>
    <p class="mt-8 mb-16 font-semibild">Hello {{ user?.email }}</p>

    <h1 class="text-black text-3xl font-semibold">Your Notes</h1>
    <p class="font-bold">
      Lorem ipsum dolor sit amet consectetur adipisicing elit. Perferendis
      aperiam numquam voluptatibus.
    </p>
  </div>
</template>
