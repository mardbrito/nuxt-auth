<script setup lang="ts">
async function signOut() {
  await authClient.signOut();
  navigateTo("/");
}
</script>

<template>
  <button @click="signOut">
    Sign Out
  </button>
</template>