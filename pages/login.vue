<script setup lang="ts">
definePageMeta({
  middleware: ['auth'],
});
const email = ref('');
const password = ref('');
const isSignUp = ref(false);
const errorMsg = ref(null);
const client = useSupabaseClient();

const signUp = async () => {
  try {
    const { user, error } = await client.auth.signUp({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
  } catch (error) {
    errorMsg.value = error.message;
    setTimeout(() => {
      errorMsg.value = null;
    }, 3000);
    console.log('user', user);
    console.log('error', error);
  }
};

const login = async () => {
  try {
    const { user, error } = await client.auth.signIn({
      email: email.value,
      password: password.value,
    });
    if (error) throw error;
  } catch (error) {
    errorMsg.value = `Error: ${error.message}`;
    setTimeout(() => {
      errorMsg.value = null;
    }, 3000);
    console.log('user', user);
    console.log('error', error);
  }
};

const user = useSupabaseUser();
onMounted(() => {
  watchEffect(() => {
    if (user.value) {
      navigateTo('/dashboard');
    }
  });
});
</script>

<template>
  <div class="max-w-lg mx-auto mt-8">
    <h1 class="font-black text-black text-center">Nuxt Login</h1>
    <div v-if="errorMsg" class="mb-10 p-4 rounded-md bg-light-grey shadow-lg">
      <p class="text-red-500">{{ errorMsg }}</p>
    </div>
    <form
      @submit.prevent="() => (isSignUp ? signUp() : login())"
      class="flex flex-col gap-2 mt-16"
    >
      <input
        type="email"
        placeholder="Email"
        required
        v-model="email"
        class="p-3 text-black rounded mb-2"
      />
      <input
        type="password"
        required
        placeholder="Password"
        v-model="password"
        class="p-3 text-black rounded bg-gray-200 mb-2"
      />
      <button
        type="submit"
        class="p-4 font-medium text-white bg-sky-500 rounded hover:bg-sky-700"
      >
        <span v-if="isSignUp"> Sign up </span>
        <span v-else> Log in </span>
      </button>
    </form>
    <button
      @click="isSignUp = !isSignUp"
      class="w-full mt-8 text-sm text-center underline text-slate-600"
    >
      <span v-if="isSignUp"> Have an account? Log in instead </span>
      <span v-else> Create a new account </span>
    </button>
  </div>
</template>
