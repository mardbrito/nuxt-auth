<script setup lang="ts">

const email = ref("");
const password = ref("");
const error = ref("");
const loading = ref(false);

async function handleSignIn() {
  error.value = "";
  loading.value = true;

  const { error: signInError } = await authClient.signIn.email({
    email: email.value,
    password: password.value,
  });

  if (signInError) {
    error.value = signInError.message ?? "Invalid credentials";
    loading.value = false;
    return;
  }

  // Invalidate cached session so middleware's useSession(useFetch) refetches
  clearNuxtData();
  navigateTo("/dashboard");
}
</script>

<template>
  <div class="flex min-h-screen items-center justify-center p-4">
    <div class="w-full max-w-md">
      <div>
        <h1 class="text-xl font-semibold">Sign In</h1>
      </div>

      <form class="space-y-4" @submit.prevent="handleSignIn">
        <div v-if="error" />

        <label label="Email" required>
          <input v-model="email" type="email" placeholder="you@example.com" required />
        </label>

        <label label="Password" required>
          <input v-model="password" type="password" placeholder="Your password" required />
        </label>

        <button type="submit" :loading="loading">
          {{ loading ? "Signing in..." : "Sign In" }}
        </button>
      </form>

      <GithubLogin />

      <div>
        <p class="text-center text-sm text-muted">
          Don't have an account?
          <NuxtLink to="/register" variant="link" size="sm" class="p-0">
            Sign up
          </NuxtLink>
        </p>
      </div>
    </div>
  </div>
</template>