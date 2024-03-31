<script setup>
import {reactive, ref} from 'vue'
import axios from 'axios'


const form = ref({
  email: '',
  password: ''
})

const errors = reactive({
  emailError: '',
  passwordError: ''
})

const login = async () => {
  try {
    const response = await axios.post('login', {
      email: form.value.email,
      password: form.value.password
    })

    console.log(response.status)
  } catch (err) {
    if (err.response.data.errors['email'])
      errors.emailError = err.response.data.errors['email'][0]

    if (err.response.data.errors['password'])
      errors.passwordError = err.response.data.errors['password'][0]
  }
}
</script>

<template>
  <div class="flex min-h-full flex-col justify-center px-6 py-12 lg:px-8">
    <div class="sm:mx-auto sm:w-full sm:max-w-sm">
      <img class="mx-auto h-10 w-auto" src="./../assets/logo.png" alt="Yesaya Software">
      <h2 class="mt-10 text-center text-2xl font-bold leading-9 tracking-tight text-gray-900">Sign in to your
        account</h2>
    </div>

    <div class="mt-10 sm:mx-auto sm:w-full sm:max-w-sm">
      <form class="space-y-6" @submit.prevent="login">
        <div>
          <label for="email" class="block text-sm font-medium leading-6 text-gray-900">Email address</label>

          <div class="mt-2">
            <input id="email"
                   name="email"
                   type="email"
                   v-model="form.email"
                   autocomplete="email"
                   class="block w-full rounded-md border-0 py-1.5 shadow-sm ring-1 ring-inset  focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6"
                   :class="[errors.emailError ? ' text-red-900 ring-red-300 placeholder:text-red-300 focus:ring-red-500' : ' text-gray-900 ring-gray-300 placeholder:text-gray-400 focus:ring-blue-600']">
          </div>

          <p v-if="errors.emailError" class="mt-2 text-sm text-red-600" id="email-error">{{ errors.emailError }}</p>
        </div>

        <div>
          <div class="flex items-center justify-between">
            <label for="password" class="block text-sm font-medium leading-6 text-gray-900">Password</label>
            <div class="text-sm">
              <a href="#" class="font-semibold text-blue-600 hover:text-blue-500">Forgot password?</a>
            </div>
          </div>

          <div class="mt-2">
            <input id="password"
                   name="password"
                   type="password"
                   v-model="form.password"
                   autocomplete="current-password"
                   class="block w-full rounded-md border-0 py-1.5 shadow-sm ring-1 ring-inset focus:ring-2 focus:ring-inset sm:text-sm sm:leading-6"
                   :class="[errors.passwordError ? ' text-red-900 ring-red-300 placeholder:text-red-300 focus:ring-red-500' : ' text-gray-900 ring-gray-300 placeholder:text-gray-400 focus:ring-blue-600']">
          </div>

          <p v-if="errors.passwordError" class="mt-2 text-sm text-red-600" id="email-error">{{
              errors.passwordError
            }}</p>
        </div>

        <div>
          <button type="submit"
                  class="flex w-full justify-center rounded-md bg-blue-600 px-3 py-1.5 text-sm font-semibold leading-6 text-white shadow-sm hover:bg-blue-500 focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-blue-600">
            Sign in
          </button>
        </div>
      </form>

      <p class="mt-10 text-center text-sm text-gray-500">
        Not a member?
        <router-link :to="{name: 'Register'}" class="font-semibold leading-6 text-blue-600 hover:text-blue-500">Register
          now
        </router-link>
      </p>
    </div>
  </div>

</template>

<style scoped>

</style>