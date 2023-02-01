<script setup lang="ts">
const user = useSupabaseUser();
const client = useSupabaseClient();
</script>

<template>
  <header class="bg-sky-500">
    <div class="container flex items-center justify-between w-full py-6">
      <nav class="ml-4 text-sm font-medium flex items-center">
        <a href="/" class="flex items-center hover:opacity-80 px-4">
          <span class="text-lg font-extrabold text-white"> Supabase</span>
          <span class="mr-2 text-lg font-extrabold text-green">Nuxt</span>
        </a>
        <NuxtLink
          to="/about"
          class="
            px-2
            py-1
            ml-auto
            mr-1
            text-base
            font-medium
            rounded
            text-white
            hover:text-gray-100
          "
          >About</NuxtLink
        >
        <NuxtLink
          to="/projects"
          v-if="user"
          class="
            px-2
            py-1
            ml-auto
            mr-1
            text-base
            font-medium
            rounded
            text-white
            hover:text-gray-100
          "
          >Projects</NuxtLink
        >
      </nav>
      <div class="flex items-center">
        <NuxtLink
          to="/dashboard"
          v-if="user"
          class="
            px-2
            py-1
            ml-auto
            mr-1
            text-base
            font-medium
            rounded
            text-white
            hover:text-gray-100
          "
          >Dashboard</NuxtLink
        >
        <NuxtLink
          to="/login"
          v-if="!user"
          class="
            px-2
            py-1
            ml-auto
            text-base
            font-medium
            rounded
            text-white
            hover:text-gray-100
          "
          >Login</NuxtLink
        >
        <button
          v-if="user"
          @click="client.auth.signOut()"
          class="px-2 py-1 text-sm font-medium rounded"
        >
          Log out
        </button>
      </div>
    </div>
  </header>
</template>
