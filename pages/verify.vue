<template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div class="relative py-3 sm:max-w-xl sm:mx-auto">
        <div class="absolute inset-0 bg-gradient-to-r from-green-200 to-blue-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
          <div class="max-w-md mx-auto text-center">
            <h1 class="text-2xl font-semibold mb-4">{{ message || 'Verifying your account...' }}</h1>
            <p v-if="!loginButtonVisible" class="text-gray-700 mb-6">Please wait while we verify your account.</p>
            <p v-if="loginButtonVisible" class="text-gray-700 mb-6">Thank you for verifying your account. You may now log in.</p>
            <div class="flex justify-center space-x-4" v-if="loginButtonVisible">
              <nuxt-link to="/login" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700 transition">
                Log In
              </nuxt-link>
            </div>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref, onMounted } from 'vue';
  import { useRoute } from 'vue-router';
  
  const route = useRoute();
  const message = ref('');
  const loginButtonVisible = ref(false);
  
  onMounted(async () => {

    const token = route.query.token;    // Get token from query parameter

    console.log("Token to send:", token); //token to send to thw backend
  
    if (token) {
      try {
        const response = await fetch('http://localhost:3005/verifyuseremail', {
          method: 'POST',
          headers: { 'Content-Type': 'application/json' },
          body: JSON.stringify({ token }),
        });
  
        const data = await response.json();
        console.log(data);
        message.value = data.message;
        loginButtonVisible.value = true; // Display login button on successful verification
      } catch (error) {
        message.value = 'Verification failed. Please try again.';
        console.error(error);
      }
    } else {
      message.value = 'Invalid verification link.';
    }
  });
  </script>
  
  <style scoped>
  /* Optional: Customize additional styles if needed */
  </style>
  