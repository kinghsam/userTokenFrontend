<template>
  <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
    <div class="relative py-3 sm:max-w-xl sm:mx-auto">
      <div class="absolute inset-0 bg-gradient-to-r from-amber-100 -400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
      <div class="relative px-6 py-10 bg-white shadow-lg sm:rounded-3xl sm:px-12 sm:py-16">
        <div class="max-w-md mx-auto">
          <!-- Form title -->
          <h1 class="text-3xl font-semibold mb-6 text-left">Reset Password</h1>
          
          <form @submit.prevent="submitForm" class="space-y-6">
            <!-- Password Input -->
            <div class="relative mb-6">
              <input
                type="password"
                id="password"
                v-model="form.password"
                required
                class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                placeholder="Password"
              />
              <label
                for="password"
                class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
              >
                Password
              </label>
            </div>

            <!-- Confirm Password Input -->
            <div class="relative mb-6">
              <input
                type="password"
                id="confirmPassword"
                v-model="form.confirmPassword"
                required
                class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                placeholder="Confirm Password"
              />
              <label
                for="confirmPassword"
                class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
              >
                Confirm Password
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
          <p v-if="errorMessage" class="text-red-500 mt-4 text-center">{{ errorMessage }}</p>
        
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// Ensure to import Vue Router in your main.js or main.ts
export default {
  data() {
    return {
      form: {
        password: '',
        confirmPassword: ''
      },
      Message: '',
      errorMessage: '',
    };
  },

  methods: {
    async submitForm() {
      // Clear previous messages
      this.Message = '';
      this.errorMessage = '';

      // Check if passwords match
      if (this.form.password !== this.form.confirmPassword) {
        this.errorMessage = 'Passwords do not match!';
        return; // Prevent form submission
      }

      // Accessing route parameters using this.$route
      const token = this.$route.query.token;
      const email = this.$route.query.email;

      // Check if token or email are missing
      if (!token || !email) {
        this.errorMessage = 'Invalid request. Missing token or email.';
        return;
      }

      // Make the API request to reset the password
      try {
        console.log("Account email to reset and token:", token, email, this.form.password);

        const response = await fetch('http://localhost:3005/forgetpassword/reset', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            email,
            token,
            newPassword: this.form.password,
          }),
        });

        if (!response.ok) {
          throw new Error('Failed to reset password. Please try again.');
        }

        const data = await response.json();
        console.log('API response:', data);
        console.log('API response message:', data.message);

        // Handle response success or failure


        if (data.message) {
          this.Message = 'Password reset successfully!';
        } else {
          this.errorMessage = 'Failed to reset password. Please try again.';
        }
      } catch (error) {
        console.error('Error during API call:', error);
        this.errorMessage = 'An error occurred. Please try again later.';
      }
    },
  },

  // Optionally check for the token and email on mounted
  mounted() {
    const token = this.$route.query.token;
    const email = this.$route.query.email;

    console.log('Token and email from route:', token, email);

    // Validate route params when the component is mounted
    if (!token || !email) {
      this.errorMessage = 'Invalid or missing token and email.';
    }
  },
};
</script>

<style scoped>
</style>
