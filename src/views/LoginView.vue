<template>
  <div class="flex items-center justify-center min-h-screen bg-gray-100">
    <div class="w-full max-w-md p-8 space-y-8 bg-white shadow-md rounded-lg">
      <h1 class="text-3xl font-semibold text-center">Login to Hem's Ride</h1>
      <form @submit.prevent="handleLogin" class="space-y-6">
        <div>
          <!-- <label for="phone" class="block text-sm font-medium text-gray-700">Phone Number</label> -->
          <input
            type="text"
            id="phone"
            v-model="credentials.phone"
            required
            placeholder="Enter your phone number"
            class="mt-1 block w-full px-3 py-2 rounded-md border border-gray-300 shadow-sm focus:ring-black focus:border-black"
          />
        </div>
        <div>
          <button
            type="submit"
            :disabled="loading"
            class="w-full flex justify-center py-2 px-4 border border-transparent rounded-md shadow-sm text-sm font-medium text-white bg-black hover:bg-slate-500 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-black disabled:opacity-50"
          >
            <span v-if="!loading">Continue</span>
            <span v-else>Loading...</span>
          </button>
        </div>
        <div v-if="error" class="text-red-500 text-sm">
          {{ error }}
        </div>
      </form>
    </div>
  </div>
</template>

<script setup>
import { reactive, ref } from 'vue'
import axios from 'axios'

const credentials = reactive({
  phone: ''
})
const loading = ref(false)
const error = ref('')

const handleLogin = async () => {
  error.value = ''
  loading.value = true
  try {
    const response = await axios.post('http://localhost/api/login', credentials)
    console.log(response.data)
    // Handle successful login (e.g., redirect to dashboard)
  } catch (err) {
    error.value = 'Failed to login. Please check your phone number and try again.'
    console.error(err)
  } finally {
    loading.value = false
  }
}
</script>

<style>
body {
  font-family: 'Roboto', sans-serif;
}
</style>
