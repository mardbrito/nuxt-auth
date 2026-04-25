<script setup lang="ts">
const session = authClient.useSession();
</script>

<template>
  <h2>Welcome to dashboard</h2>
  <div v-if="session.isPending">
    Checking session...
  </div>
  <div v-else-if="session.data" class="max-w-md">
    <div>
      <p class="font-medium">Welcome, {{ session.data.user.name }}</p>
      <p class="font-sm text-muted">{{ session.data.user.email }}</p>
    </div>
    <SignOut />
  </div>
  <div v-else>
    <NuxtLink to="/login"> Sign In </NuxtLink>
  </div>
</template>