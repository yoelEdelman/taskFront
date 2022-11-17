<template>
  <!--
  This example requires some changes to your config:

  ```
  // tailwind.config.js
  module.exports = {
    // ...
    plugins: [
      // ...
      require('@tailwindcss/forms'),
    ],
  }
  ```
-->
  <form class="space-y-8 divide-y divide-gray-200">
    <div class="space-y-8 divide-y divide-gray-200 sm:space-y-5">
      <div class="space-y-6 pt-8 sm:space-y-5 sm:pt-10">
        <div>
          <h3 class="text-lg font-medium leading-6 text-gray-900">Personal Information</h3>
          <p class="mt-1 max-w-2xl text-sm text-gray-500">Use a permanent address where you can receive mail.</p>
        </div>
        <div class="space-y-6 sm:space-y-5">
          <div class="sm:grid sm:grid-cols-3 sm:items-start sm:gap-4 sm:border-t sm:border-gray-200 sm:pt-5">
            <label for="name" class="block text-sm font-medium text-gray-700 sm:mt-px sm:pt-2">Name</label>
            <div class="mt-1 sm:col-span-2 sm:mt-0">
              <input v-model.trim="user.name" type="text" name="name" id="name" autocomplete="given-name" class="block w-full max-w-lg rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:max-w-xs sm:text-sm">
            </div>
          </div>

          <div class="sm:grid sm:grid-cols-3 sm:items-start sm:gap-4 sm:border-t sm:border-gray-200 sm:pt-5">
            <label for="email" class="block text-sm font-medium text-gray-700 sm:mt-px sm:pt-2">Email address</label>
            <div class="mt-1 sm:col-span-2 sm:mt-0">
              <input v-model.trim="user.email" id="email" name="email" type="email" autocomplete="email" class="block w-full max-w-lg rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm">
            </div>
          </div>
        </div>
      </div>
    </div>

    <div class="pt-5">
      <div class="flex justify-end">
        <nuxt-link to="/users" type="button" class="rounded-md border border-gray-300 bg-white py-2 px-4 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Back to users</nuxt-link>
        <button @click="submitForm" type="submit" class="ml-3 inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Save</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      user: {}
    }
  },
  async fetch() {
    this.user = await fetch('http://localhost:8888/api/users/' + this.$route.params.id)
      .then(res => res.json())
  },
  methods: {
    submitForm() {
      this.$axios.$put('http://localhost:8888/api/users/' + this.user.id, this.user)
        // .then(this.user = this.user)
    }
  }
}
</script>
