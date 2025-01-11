<template>
  <div class="flex min-h-screen bg-gray-100">
    <!-- Sidebar -->
    <aside class="w-64 bg-gradient-to-b from-amber-100 to-sky-500 text-white flex flex-col">
      <div class="p-6">
        <h1 class="text-2xl font-bold">Dashboard</h1>
      </div>
      <nav class="flex-grow">
        <ul class="space-y-4 px-4">
          <li>
            <a href="#" class="block py-2 px-3 rounded hover:bg-amber-200 hover:text-gray-800">
              Profile
            </a>
          </li>
          <li>
            <a href="#" class="block py-2 px-3 rounded hover:bg-amber-200 hover:text-gray-800">
              Settings
            </a>
          </li>
          <li>
            <a href="#" class="block py-2 px-3 rounded hover:bg-amber-200 hover:text-gray-800">
              Analytics
            </a>
          </li>
          <li>
            
          <nuxt-link to ="/login" class="block py-2 px-3 rounded hover:bg-amber-200 hover:text-gray-800">
              Logout
            </nuxt-link>
          </li>
        </ul>
      </nav>
    </aside>

    <!-- Main Content -->
    <div class="flex-1 flex flex-col">
      <!-- Header -->
      <header class="bg-gradient-to-r from-amber-100 via-sky-100 to-sky-500 shadow px-6 py-4 flex justify-between items-center">
        <h2 class="text-lg font-semibold text-gray-800">Welcome, {{ firstName }}</h2>
        <div class="flex items-center space-x-4">
          <span class="text-gray-700">{{ email }}</span>
          <div class="w-10 h-10 bg-gray-300 rounded-full flex items-center justify-center">
            <span class="text-sm font-bold text-blue-800"></span>
          </div>
        </div>
      </header>

      <!-- Content Area -->
      <main class="flex-1 p-6 space-y-6">
        <!-- Dashboard Cards -->
        <div class="grid grid-cols-1 md:grid-cols-3 gap-6">
          <!-- Card 1 -->
          <div class="p-6 bg-white shadow-lg rounded-lg border-l-4 border-amber-400">
            <h3 class="text-xl font-bold text-gray-800">Profile</h3>
            <p class="mt-2 text-gray-600">First Name: {{ firstName }}</p>
            <p class="mt-2 text-gray-600">Last Name: {{ lastName }}</p>
          </div>
          <!-- Card 2 -->
          <div class="p-6 bg-white shadow-lg rounded-lg border-l-4 border-sky-400">
            <h3 class="text-xl font-bold text-gray-800">Notifications</h3>
            <p class="mt-2 text-gray-600">No new notifications</p>
          </div>
          <!-- Card 3 -->
          <div class="p-6 bg-white shadow-lg rounded-lg border-l-4 border-green-400">
            <h3 class="text-xl font-bold text-gray-800">Settings</h3>
            <p class="mt-2 text-gray-600">Customize your dashboard</p>
          </div>
        </div>

    
      </main>
    </div>
  </div>
</template>

<script setup lang="ts">

interface ProfileResponse {
  data: { firstName: string; lastName: string; email: string };
  successfull: boolean;
  message: string;
}

const firstName = ref('');
const lastName = ref('');
const email = ref('');

async function getUserDetails() {


  const token = localStorage.getItem('JWT');

  try {
    const response = await fetch('http://localhost:3005/verifyuseremail/getprofile', {
      headers: {
        Authorization: `Bearer ${token}`,
      },
    });

    const res: ProfileResponse = await response.json();

    console.log("User Details:", res);

    if (res.successfull === true) {

      firstName.value = res.data.firstName;

      console.log("First Name:", firstName.value);

      lastName.value = res.data.lastName;
      email.value = res.data.email;
    }
  } catch (error) {
    console.error('Error fetching user details:', error);
  }
}

onMounted(() => {
  getUserDetails();
});
</script>

<style scoped>
/* No additional styles, fully Tailwind CSS-driven */
</style>
