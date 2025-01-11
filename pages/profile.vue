<template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div class="relative py-3 sm:max-w-3xl sm:mx-auto">
        <div class="absolute inset-0 bg-gradient-to-r from-amber-100 -400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div class="relative px-8 py-10 bg-white shadow-lg sm:rounded-3xl sm:px-16 sm:py-20">
          <div class="max-w-3xl mx-auto">
            <h1 class="text-3xl font-semibold mb-6 text-left">User Information</h1>

            <form  @submit.prevent="handleProfile" class="divide-y divide-gray-200 space-y-6">
              <div class="text-base leading-6 text-gray-700 sm:text-lg sm:leading-7">
                <!-- First Name -->
                <div class="relative mb-6">
                  <input
                    v-model="firstName"
                    id="firstName"
                    name="firstName"
                    type="text"
                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                    placeholder="First Name"
                  />
                  <label
                    for="firstName"
                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                  >First Name</label>
                </div>
  
                <!-- Last Name -->
                <div class="relative mb-6">
                  <input
                    v-model="lastName"
                    id="lastName"
                    name="lastName"
                    type="text"
                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                    placeholder="Last Name"
                  />
                  <label
                    for="lastName"
                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                  >Last Name</label>
                </div>
  
                <!-- Email -->
                <!-- <div class="relative mb-6">
                  <input
                    v-model="email"
                    id="email"
                    name="email"
                    type="email"
                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                    placeholder="Email Address"
                  />
                  <label
                    for="email"
                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                  >Email Address</label>
                </div>
   -->
                <!-- Gender -->
                <div class="relative mb-6">
                  <label for="gender" class="text-sm text-gray-600">Gender</label>
                  <select
                    v-model="gender"
                    id="gender"
                    name="gender"
                    class="mt-2 h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                  >
                    <option value="" disabled>Select Gender</option>
                    <option value="Male">Male</option>
                    <option value="Female">Female</option>
                    <option value="other">Other</option>
                  </select>
                </div>
  
                <!-- Phone Number -->
                <div class="relative mb-6">
                  <input
                    v-model="phone"
                    id="phone"
                    name="phone"
                    type="tel"
                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                    placeholder="Phone Number"
                  />
                  <label
                    for="phone"
                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                  >Phone Number</label>
                </div>
  
                <!-- Address -->
                <div class="relative mb-6">
                  <textarea
                    v-model="address"
                    id="address"
                    name="address"
                    rows="3"
                    class="peer placeholder-transparent w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                    placeholder="Address"
                  ></textarea>
                  <label
                    for="address"
                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                  >Address</label>
                </div>
  
                <!-- Submit Button -->
                <div class="relative flex justify-center items-center">
                  <button
                    type="submit"
                    class="bg-blue-500 text-white px-6 py-3 rounded-md font-semibold hover:bg-blue-600 transition"
                  >
                    Complete Profile
                  </button>

                  <p v-if="errorMsg" class="text-red-500 mt-4 text-center">{{ errorMsg }}</p>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </template>
  
  <script setup lang="ts">
 

 interface profileRespone {

successfull: boolean;
message: string;
}

 
 let email= ref("");
  const firstName =ref("");
  const lastName = ref("");
  const phone = ref("");
  const address = ref(" ");
  const gender = ref("");
  const errorMsg = ref("");

  const router=useRouter();

  const handleProfile= async () => {
   email.value = localStorage.getItem("email");

    try {
      const response = await fetch('http://localhost:3005/profile', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
            
          email: email.value,
          firstName: firstName.value,
          lastName: lastName.value,
          phone: phone.value,
          address: address.value,
          gender: gender.value,

        }),

      });
  
      const res: profileRespone = await response.json();

      console.log(res);

      
      if(res.successfull === true){

        router.push('/user');

      }
     else{
      if(res.successfull === false){
        errorMsg.value = res.message;

        console.log("error message value", errorMsg.value);
      }
     }


    } catch (error:any) {
      errorMsg.value = error.message;
      console.error("Error signing up:", error);
    }
  };

 

  </script>
  
  <style scoped>
  /* Add additional custom styles here if needed */
  </style>
  