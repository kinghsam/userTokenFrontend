<template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div class="relative py-3 sm:max-w-xl sm:mx-auto">
        <div class="absolute inset-0 bg-gradient-to-r from-green-200 to-blue-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
          <div class="max-w-md mx-auto text-center">
            <h1 class="text-2xl font-semibold mb-4">Account Confirmed!</h1>
            <p class="text-gray-700 mb-6">Thank you for verifying your account. You may now log in.</p>
            <div class="flex justify-center space-x-4">
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
  // No additional logic needed for this confirmation page
  </script>
  
  <style scoped>
  /* Optional: Customize additional styles */
  </style>
  