<template>
  <div class="container text-center mt-5">
    <h1>Login</h1>
    <button class="btn btn-primary" @click="login">Login with Google</button>
  </div>
</template>

<script setup>
import { loginWithGoogle, auth } from '../firebase';
import { onAuthStateChanged } from 'firebase/auth';
import { useRouter } from 'vue-router';

const router = useRouter();

onAuthStateChanged(auth, (user) => {
  if (user) {
    router.push('/home');
  }
});

const login = async () => {
  await loginWithGoogle();
};
</script>
