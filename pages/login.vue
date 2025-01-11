


<!-- <template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
      <div class="relative py-3 sm:max-w-xl sm:mx-auto">
        <div class="absolute inset-0 bg-gradient-to-r from-amber-100 -400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
        <div class="relative px-4 py-10 bg-white shadow-lg sm:rounded-3xl sm:p-20">
          <div class="max-w-md mx-auto">
            <div>
              <h1 class="text-2xl font-semibold">Login</h1>
            </div>
            <form class="divide-y divide-gray-200" >
  
              <div class="py-8 text-base leading-6 space-y-4 text-gray-700 sm:text-lg sm:leading-7">
                <div class="relative">
                  <input
                    v-model="email"
                   
                    id="email"
                    name="email"
                    type="text"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="Email address"
                  />
                  <label
                    for="email"
                    class="absolute left-0 -top-3.5 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-440 peer-placeholder-shown:top-2 transition-all peer-focus:-top-3.5 peer-focus:text-gray-600 peer-focus:text-sm"
                    >Email Address</label
                  >
                </div>
                <div class="relative">
                  <input
                    v-model="password"
                
                    id="password"
                    name="password"
                    type="password"
                    class="peer placeholder-transparent h-10 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-rose-600"
                    placeholder="Password"
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
                  >
                    Sign-In
                  </button>
  
                  <nuxt-link to="/signup" class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700 transition">
                SignUp
              </nuxt-link>
                </div>
              </div>
            </form>
             <p v-if="errorMsg" class="text-red-500">{{ errorMsg }}</p>
             <p  class="text-red-500">error message to show here</p>
          </div>
        </div>
      </div>
    </div>
  </template> --> 

  <template>
    <div class="min-h-screen bg-gray-100 py-6 flex flex-col justify-center sm:py-12">
        <div class="relative py-3 sm:max-w-xl sm:mx-auto">
            <div class="absolute inset-0 bg-gradient-to-r from-amber-100 -400 to-sky-500 shadow-lg transform -skew-y-6 sm:skew-y-0 sm:-rotate-6 sm:rounded-3xl"></div>
            <div class="relative px-6 py-10 bg-white shadow-lg sm:rounded-3xl sm:px-12 sm:py-16">
                <div class="max-w-md mx-auto">
                    <!-- Aligned the title to the left -->
                    <div>
                        <h1 class="text-3xl font-semibold mb-6 text-left">Login</h1>
                    </div>
                    <form class="divide-y divide-gray-200 space-y-6"   @submit.prevent="handleLogin"  >
                        <div class="text-base leading-6 text-gray-700 sm:text-lg sm:leading-7">
                            <div class="relative mb-6">
                                <input
                                    v-model="email"
                                    id="email"
                                    name="email"
                                    type="text"
                                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                                    placeholder="Email address"
                                />
                                <label
                                    for="email"
                                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                                >Email Address</label>
                            </div>
                            <div class="relative mb-6">
                                <input
                                    v-model="password"
                                    id="password"
                                    name="password"
                                    type="password"
                                    class="peer placeholder-transparent h-12 w-full border-b-2 border-gray-300 text-gray-900 focus:outline-none focus:border-blue-500"
                                    placeholder="Password"
                                />
                                <label
                                    for="password"
                                    class="absolute left-0 -top-4 text-gray-600 text-sm peer-placeholder-shown:text-base peer-placeholder-shown:text-gray-400 peer-placeholder-shown:top-3 transition-all peer-focus:-top-4 peer-focus:text-gray-600 peer-focus:text-sm"
                                >Password</label>
                            </div>

                            <div class="flex space-x-4 mb-4">
                                <button @click="handleLogin()"
                                    type="submit"
                                    class="w-full bg-blue-500 text-white px-4 py-3 rounded-md font-semibold hover:bg-blue-600 transition"
                                >
                                    Sign-In
                                </button>

                                <nuxt-link to="/signup" class="w-full bg-blue-500 text-white px-4 py-3 rounded-md font-semibold text-center hover:bg-blue-600 transition">
                                    SignUp
                                </nuxt-link>
                            </div>

                            <!-- Forgot Password Link -->
                            <div class="text-center">
                                <nuxt-link to="/forgetPassword" class="text-blue-500 hover:text-blue-700 text-sm transition">
                                    Forgot Password?
                                </nuxt-link>
                            </div>
                        </div>
                    </form>
                    <p v-if="errorMsg" class="text-red-500 mt-4 text-center">{{ errorMsg }}</p>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">

enum onBoardingStatus {
    Unverified = "Unverified",
    Verfieid = "Verified",
    ProfileunderReview = "ProfileunderReview",
    ProfileCompleted = "ProfileCompleted",
}   
  


interface LoginRespone {

  data : {
    token: string;
    email: string;
    onBoardingLevel:boolean;
    onBoardingStatus:onBoardingStatus;
  }
  successfull: boolean;
  message: string;
}

// const jwtState = useState('JWT', () => '');

  const email = ref("");
  const password = ref("");
  const errorMsg = ref (" ");
  const successMsg = ref(null);

const router=useRouter();

  const handleLogin= async () => {
  

    try {
      const response = await fetch('http://localhost:3005/login', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          email: email.value,
          password: password.value,

        }),

      });
  
      const res: LoginRespone = await response.json();

      console.log(res);

      
      if(res.successfull === true){

        localStorage.setItem('email', res.data.email);
        localStorage.setItem('JWT', res.data.token)	;



        if(res.data.onBoardingStatus === onBoardingStatus.ProfileunderReview){ 
          router.push('/profile');
          return;
        }

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
      console.error("Error logging in:", error);
    }
  };



      
//     errorMsg.value = null;
//     successMsg.value = null;
  
//     if ( !email.value || !password.value) {
//       errorMsg.value = "All fields are required.";
//       return;
//     }
  
// localStorage.setItem("username", "my name is  goddy");

// localStorage.getItem("username");


</script>

<style>

</style>