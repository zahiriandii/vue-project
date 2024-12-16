<script setup>

  import axios from 'axios';  
  import { reactive } from 'vue';
  import router from '@/router';
  import { RouterLink } from 'vue-router';
  const userData = reactive({
    email: '',
    password: ''
  });

const checkUser = async () =>
{
    try {
        const response = await axios.post('http://localhost:5000/api/logIn',{
            email: userData.email,
            password: userData.password
        });

        router.push('/');
        console.log('LogIn successful',response.data);
    } catch (error) {
        console.log('LogIn error',error);
    }
}

</script>

<template>
<body class="bg-gray-100 flex items-center justify-center min-h-screen">

<div class="w-full max-w-md bg-white p-8 rounded-lg shadow-lg">
  <div class="text-center mb-6">
    <h1 class="text-2xl font-bold text-gray-800">Welcome</h1>
    <div class="w-10 h-10 mx-auto mt-2 flex items-center justify-center bg-gray-200 rounded-full">
      <span class="text-gray-600 font-bold text-lg">A</span>
    </div>
  </div>

  <form @submit.prevent="checkUser">
    <!-- Email Field -->
    <div class="mb-4">
      <label for="email" class="block text-gray-600 font-medium mb-2">Email</label>
      <input v-model="userData.email" type="email" id="email" placeholder="Enter your email"
        class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" />
    </div>

    <!-- Password Field -->
    <div class="mb-6 relative">
      <label for="password" class="block text-gray-600 font-medium mb-2">Password</label>
      <input v-model="userData.password" type="password" id="password" placeholder="Enter your password"
        class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-400" />
      <!-- Eye Icon Placeholder -->
      <span class="absolute inset-y-0 right-3 flex items-center text-gray-400 cursor-pointer">
        👁️
      </span>
    </div>

    <!-- Login Button -->
    <button type="submit"
      class="w-full py-2 rounded-lg bg-gradient-to-r from-blue-400 to-purple-500 text-white font-semibold hover:opacity-90 transition-all">
      LOGIN
    </button>
  </form>

  <!-- Sign Up Prompt -->
  <p class="text-center text-gray-600 mt-6">
    Don't have an account?
    <RouterLink to="/signUp" class="text-blue-500 font-medium hover:underline">Sign Up</RouterLink>
  </p>
</div>
</body>
</template>