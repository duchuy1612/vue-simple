<script setup lang="ts">
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const router = useRouter()
const email = ref('')
const password = ref('')
let showPassword = ref(false)
let isLoading = ref(false)
let isInvalidCred = ref(false)

function togglePasswordVisibility(){
    showPassword.value = !showPassword.value
}

function login() {
    isLoading.value = true
    router.push('/dashboard')
}

function onChange(event: any, isEmail: boolean) {
    if (isEmail) {
        email.value = event.target.value
    }
    else {
        password.value = event.target.value
    }
    isInvalidCred.value = !isInvalidCred.value
}

function forgotPassword(){
    router.push('/change-password')
}

</script>

<template>
    <div class="flex items-center justify-center h-screen w-full px-6 bg-indigo-700">
        <div class="flex flex-row w-full max-w-3xl bg-white rounded-md shadow-md">
            <div class="flex flex-col items-center justify-center basis-1/2">
                <div class="flex flex-col items-center justify-center">
                    <img
                    class="object-cover h-20 w-20"
                    src="/cube-run.png"
                    >
                    <span class="text-2xl font-semibold text-gray-700">Cube Run</span>
                </div>

                <form class="mt-4" @submit.prevent="login">
                    <label class="block">
                        <span class="text-sm text-gray-700">Email</span>
                        <input
                            v-model="email"
                            type="email"
                            placeholder="Enter your email address"
                            class="block w-full mt-1 border-gray-200 rounded-md focus:border-indigo-600 focus:ring focus:ring-opacity-40 focus:ring-indigo-500"
                            @change="onChange($event, true)"
                            required
                        >
                    </label>
            
                    <label class="block mt-3 relative items-center">
                        <span class="text-sm text-gray-700">Password</span>
                        <input
                            v-model="password"
                            v-if="showPassword"
                            type="text"
                            placeholder="Enter your password"
                            class="input block w-full mt-1 border-gray-200 rounded-md focus:border-indigo-600 focus:ring focus:ring-opacity-40 focus:ring-indigo-500 pr-10"
                            @change="onChange($event, false)"
                            required
                        >
                        <input
                            v-model="password"
                            v-else
                            type="password"
                            placeholder="Enter your password"
                            class="input block w-full mt-1 border-gray-200 rounded-md focus:border-indigo-600 focus:ring focus:ring-opacity-40 focus:ring-indigo-500 pr-10"
                            @change="onChange($event, false)"
                            required
                      >
                        <button
                          type="button"
                          class="absolute top-2/3 right-2 transform -translate-y-1/2 text-gray-600 flex items-center"
                          @click="togglePasswordVisibility"
                        >
                            <svg v-if="showPassword" 
                                xmlns="http://www.w3.org/2000/svg" 
                                width="36" 
                                height="36" 
                                viewBox="0 0 36 36"
                            >
                                <path fill="currentColor" 
                                    d="M33.62 17.53c-3.37-6.23-9.28-10-15.82-10S5.34 11.3 2 17.53l-.28.47l.26.48c3.37 6.23 9.28 10 15.82 10s12.46-3.72 15.82-10l.26-.48Zm-15.82 8.9C12.17 26.43 7 23.29 4 18c3-5.29 8.17-8.43 13.8-8.43S28.54 12.72 31.59 18c-3.05 5.29-8.17 8.43-13.79 8.43Z" 
                                    class="clr-i-outline clr-i-outline-path-1"
                                />
                                <path fill="currentColor" 
                                    d="M18.09 11.17A6.86 6.86 0 1 0 25 18a6.86 6.86 0 0 0-6.91-6.83Zm0 11.72A4.86 4.86 0 1 1 23 18a4.87 4.87 0 0 1-4.91 4.89Z" 
                                    class="clr-i-outline clr-i-outline-path-2"
                                />
                                <path fill="none" d="M0 0h36v36H0z"/>
                            </svg>
                            <svg v-else 
                                xmlns="http://www.w3.org/2000/svg" 
                                width="36" 
                                height="36" 
                                viewBox="0 0 36 36"
                            >
                                <path fill="currentColor" 
                                    d="M25.19 20.4a6.78 6.78 0 0 0 .43-2.4a6.86 6.86 0 0 0-6.86-6.86a6.79 6.79 0 0 0-2.37.43L18 13.23a4.78 4.78 0 0 1 .74-.06A4.87 4.87 0 0 1 23.62 18a4.79 4.79 0 0 1-.06.74Z" class="clr-i-outline clr-i-outline-path-1"/><path fill="currentColor" d="M34.29 17.53c-3.37-6.23-9.28-10-15.82-10a16.82 16.82 0 0 0-5.24.85L14.84 10a14.78 14.78 0 0 1 3.63-.47c5.63 0 10.75 3.14 13.8 8.43a17.75 17.75 0 0 1-4.37 5.1l1.42 1.42a19.93 19.93 0 0 0 5-6l.26-.48Z" class="clr-i-outline clr-i-outline-path-2"/><path fill="currentColor" d="m4.87 5.78l4.46 4.46a19.52 19.52 0 0 0-6.69 7.29l-.26.47l.26.48c3.37 6.23 9.28 10 15.82 10a16.93 16.93 0 0 0 7.37-1.69l5 5l1.75-1.5l-26-26Zm9.75 9.75l6.65 6.65a4.81 4.81 0 0 1-2.5.72A4.87 4.87 0 0 1 13.9 18a4.81 4.81 0 0 1 .72-2.47Zm-1.45-1.45a6.85 6.85 0 0 0 9.55 9.55l1.6 1.6a14.91 14.91 0 0 1-5.86 1.2c-5.63 0-10.75-3.14-13.8-8.43a17.29 17.29 0 0 1 6.12-6.3Z" 
                                    class="clr-i-outline clr-i-outline-path-3"
                                />
                                <path fill="none" d="M0 0h36v36H0z"/>
                            </svg>
                        </button>
                      </label>
                      
            
                    <div class="flex flex-row items-start justify-between justify-items-stretch mt-4 gap-4">
                        <div>
                            <label class="inline-flex items-center">
                                <input type="checkbox" class="text-indigo-600 border-gray-200 rounded-md focus:border-indigo-600 focus:ring focus:ring-opacity-40 focus:ring-indigo-500">
                                <span class="mx-2 text-sm text-gray-600">Remember me</span>
                            </label>
                        </div>
            
                        <div>
                        <a
                            class="block text-sm text-indigo-700 fontme hover:underline"
                            href="#"
                            @click.prevent="forgotPassword"
                        >Forgot your password?</a>
                        </div>
                    </div>
            
                    <div class="mt-6">
                        <button
                        type="submit"
                        class="w-full px-4 py-2 text-sm text-center text-white bg-indigo-600 rounded-md focus:outline-none hover:bg-indigo-500"
                        >
                        Sign in
                        </button>
                    </div>
                </form>
            </div>
            <div class="flex w-full h-full max-h-full max-w-full basis-1/2">
                <img
                    src="/Rectangle 313.png"
                    className="object-cover top-0 right-0"
                >              
            </div>
        </div>
      </div>
</template>