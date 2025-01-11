<template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div class="relative py-3 sm:max-w-xl sm:mx-auto">
        <div class="absolute inset-0 bg-gradient-to-r from-amber-100 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
          <div class="max-w-md mx-auto">
            <div>
              <h1 class="text-2xl font-semibold">Register Your Account</h1>
            </div>
            <form @submit.prevent="handleSignup" class="divide-y divide-gray-200">
              <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                <div class="relative">
                  <input
                    autocomplete="off"
                    id="username"
                    name="username"
                    type="text"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="Username"
                    v-model="username"
                    required
                  />
                  <label
                    for="username"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Username</label
                  >
                </div>
                <div class="relative">
                  <input
                    autocomplete="off"
                    id="email"
                    name="email"
                    type="email"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="Email address"
                    v-model="email"
                    required
                  />
                  <label
                    for="email"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Email Address</label
                  >
                </div>
                <div class="relative">
                  <input
                    autocomplete="off"
                    id="password"
                    name="password"
                    type="password"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="Password"
                    v-model="password"
                    required
                  />
                  <label
                    for="password"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Password</label
                  >
                </div>
                <div class="relative flex justify-between items-center">
                  <button
                    type="submit"
                    class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700 transition"
                  >Sign Up</button>
                </div>
              </div>
            </form>
            <p v-if="successMsg" class="text-green-500">{{ successMsg }}</p>
            <p v-if="errorMsg" class="text-red-500">{{ errorMsg }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const username = ref("");
  const email = ref("");
  const password = ref("");
  const errorMsg = ref(null);
  const successMsg = ref(null);
  
  const handleSignup = async () => {
    
    errorMsg.value = null;
    successMsg.value = null;
  
    if (!username.value || !email.value || !password.value) {
      errorMsg.value = "All fields are required.";
      return;
    }
  
localStorage.setItem("username", "my name is  goddy");

localStorage.getItem("username");

    try {
      const response = await fetch('http://localhost:3005/confirmemail', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          username: username.value,
          email: email.value,
          password: password.value,
        }),
      });
  
      const data = await response.json();
  
      if (!response.ok) {
        console.log('an error occurred:', data.message)
      }
  
      successMsg.value = data.message; // Expecting a success message from backend
    } catch (error) {
      errorMsg.value = error.message;
      console.error("Error signing up:", error);
    }
  };
  </script>
  
  <style scoped>
  /* Add your scoped styles here */
  </style>
  