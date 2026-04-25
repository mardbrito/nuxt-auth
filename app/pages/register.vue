<script setup lang="ts">

const name = ref("");
const email = ref("");
const password = ref("");
const error = ref("");
const loading = ref(false);

async function handleSignUp() {
  error.value = "";
  loading.value = true;

  const { error: signUpError } = await authClient.signUp.email({
    name: name.value,
    email: email.value,
    password: password.value,
  });

  if (signUpError) {
    error.value = signUpError.message ?? "Something went wrong";
    loading.value = false;
    return;
  }

  clearNuxtData();
  navigateTo("/dashboard");
}
</script>

<template>
  <div class="flex min-h-screen items-center justify-center p-4">
    <div class="w-full max-w-md">
      <div>
        <h1 class="text-xl font-semibold">Create an Account</h1>
      </div>

      <form class="space-y-4" @submit.prevent="handleSignUp">
        <div v-if="error" :description="error" />

        <label label="Name" required>
          <input v-model="name" type="text" placeholder="Your name" required />
        </label>

        <label label="Email" required>
          <input v-model="email" type="email" placeholder="you@example.com" required />
        </label>

        <label label="Password" required>
          <input v-model="password" type="password" placeholder="At least 8 characters" required />
        </label>

        <button type="submit" :loading="loading">
          {{ loading ? "Creating account..." : "Sign Up" }}
        </button>
      </form>

      <div>
        <p class="text-center text-sm text-muted">
          Already have an account?
          <NuxtLink to="/login" class="p-0">
            Sign in
          </NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>