<script setup lang="ts">
function signInWithGitHub() {
  authClient.signIn.social({
    provider: "github",
    callbackURL: "/dashboard",
  });
}
</script>

<template>
  <button block @click="signInWithGitHub">
    Continue with GitHub
  </button>
</template>