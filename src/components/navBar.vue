<script setup>
  import { RouterLink,useRoute } from 'vue-router';
  import {useUserStore} from '@/stores/userStore';
  import axios from 'axios';
  import router from '@/router';
 

  const isActiveLink = (routePath) => 
    {
      const route = useRoute();
      return route.path === routePath;
    }

    let userData = useUserStore();
    
    const logoutUser = async () =>
    {
      
      try { 
        const response = await axios.post("http://localhost:5001/api/auth/logOut");
        userData.setUser(null);
        router.push('/logIn');
      } catch (error) {
        console.log('Error while loggingOut',error);
      }
    }


</script>

<template>
  <nav class="bg-green-700 border-b border-green-500">
      <div class="mx-auto max-w-7xl px-2 sm:px-6 lg:px-8">
        <div class="flex h-20 items-center justify-between">
          <div
            class="flex flex-1 items-center justify-center md:items-stretch md:justify-start"
          >
            <!-- Logo -->
            <RouterLink class="flex flex-shrink-0 items-center mr-4" to="/">
              <img class="h-10 w-auto" src="" alt="Vue Jobs" />
              <span class="hidden md:block text-white text-2xl font-bold ml-2"
                >Vue Jobs</span
              >
            </RouterLink>
            <div class="md:ml-auto">
              <div class="flex space-x-2">
                <RouterLink
                  to="/"
                  :class="[isActiveLink('/') ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-3','py-2','rounded-md']"
                  >Home</RouterLink
                >
                <RouterLink
                  to="/jobs"
                  :class="[isActiveLink('/jobs') ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-3','py-2','rounded-md']"
                  >Jobs</RouterLink
                >
                <RouterLink
                  to="/jobs/add"
                  :class="[isActiveLink('/add-job') ? 'bg-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-3','py-2','rounded-md']"
                  >Add Job</RouterLink
                >
                <RouterLink
                v-if="!userData.user"
               to="/logIn"
               :class="[isActiveLink('/logIn') ? 'gb-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-4','py-2','rounded-md']"
              >Log In</RouterLink>
              <RouterLink
               v-if="userData.user"
               to="/hello"
               :class="[isActiveLink('/hello') ? 'gb-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-4','py-2','rounded-md']"
              >Hello {{ userData.user ? userData.user.email : ''  }}</RouterLink>
              <a
               v-if="userData.user"
               :class="[isActiveLink('/logOut') ? 'gb-green-900' : 'hover:bg-gray-900 hover:text-white','text-white','px-4','py-2','rounded-md']"
               @click="logoutUser"
              >Log Out</a>
              </div>
            </div>
            
          </div>
        </div>
      </div>
    </nav>
</template>