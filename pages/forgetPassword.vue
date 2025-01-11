<template>
  <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
    <div class="relative py-3 sm:max-w-xl sm:mx-auto">
      <div class="absolute inset-0 bg-gradient-to-r from-amber-100 -400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
      <div class="relative px-6 py-10 bg-white shadow-lg sm:rounded-3xl sm:px-12 sm:py-16">
        <div class="max-w-md mx-auto">
          <!-- Form title -->
          <h1 class="text-3xl font-semibold mb-6 text-left">Reset Password</h1>
          
          <form @submit.prevent="submitForm" class="space-y-6">
            <!-- Email Input -->
            <div class="relative mb-6">
              <input
                type="email"
                id="email"
                v-model="form.email"
                required
                class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                placeholder="Email address"
              />
              <label
                for="email"
                class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
              >
                Email Address
              </label>
            </div>
            
            <!-- Submit Button -->
            <div class="flex justify-center">
              <button
                type="submit"
                class="w-full bg-blue-500 text-white px-4 py-3 rounded-md font-semibold hover:bg-blue-600 transition"
              >
                RESET PASSWORD
              </button>
            </div>
          </form>
          
          <!-- Optional Success/Error Message -->
          <p v-if="Message" class="text-green-500 mt-4 text-center">{{ Message }}</p>
        
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      form: {
        email: '',
        password: ''
      },
      Message: '',  // Declare Message as a reactive property
    };
  },
  methods: {
    async submitForm() {
      // Handle form submission logic here
      this.Message = '';  // Clear the message before submitting

      try {
        const response = await fetch('http://localhost:3005/forgetpassword', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            email: this.form.email,
          }),
        });

        const data = await response.json();
        console.log(data);

        this.Message = data.message;  // Correctly assign the message with 'this'

      } catch (error) {
        console.error(error);
      }
      console.log('Form Submitted:', this.form);
    },
  },
};
</script>

<style>
</style>
