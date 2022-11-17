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
    <div class="space-y-8 sm:space-y-5">
      <div class="space-y-6 sm:space-y-5">
        <div>
          <h3 class="text-lg font-medium leading-6 text-gray-900">Update task</h3>
        </div>

        <div class="space-y-6 pt-8 sm:space-y-5 sm:pt-10">
          <div class="space-y-6 sm:space-y-5">
            <div class="sm:grid sm:grid-cols-3 sm:items-start sm:gap-4 sm:border-t sm:border-gray-200 sm:pt-5">
              <label for="title" class="block text-sm font-medium text-gray-700 sm:mt-px sm:pt-2">Title</label>
              <div class="mt-1 sm:col-span-2 sm:mt-0">
                <input v-model="task.title" type="text" name="title" id="title" autocomplete="given-name" class="block w-full max-w-lg rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:max-w-xs sm:text-sm">
              </div>
            </div>
          </div>
        </div>

        <div class="space-y-6 sm:space-y-5">
          <div class="sm:grid sm:grid-cols-3 sm:items-start sm:gap-4 sm:pt-5">
            <label for="description" class="block text-sm font-medium text-gray-700 sm:mt-px sm:pt-2">Description</label>
            <div class="mt-1 sm:col-span-2 sm:mt-0">
              <textarea v-model="task.description" id="description" name="description" rows="3" class="block w-full max-w-lg rounded-md border-gray-300 shadow-sm focus:border-indigo-500 focus:ring-indigo-500 sm:text-sm"></textarea>
            </div>
          </div>
        </div>
      </div>



      <div class="divide-y divide-gray-200   sm:pt-10">
        <div class="space-y-6 divide-y divide-gray-200 sm:space-y-5">
          <div class="pt-6 sm:pt-5">
            <div role="group" aria-labelledby="label-email">
              <div class="sm:grid sm:grid-cols-3 sm:items-baseline sm:gap-4">
                <div>
                  <div class="text-base font-medium text-gray-900 sm:text-sm sm:text-gray-700" id="label-email">Status</div>
                </div>
                <div class="mt-2 sm:col-span-2 sm:mt-0">
                  <div class="max-w-lg space-y-4">
                    <div class="relative flex items-start">
                      <div class="flex h-5 items-center">
                        <input v-model="task.status" id="status" name="status" type="checkbox" class="h-4 w-4 rounded border-gray-300 text-indigo-600 focus:ring-indigo-500">
                      </div>
                      <div class="ml-3 text-sm">
                        <label for="status" class="font-medium text-gray-700">Done ?</label>
                      </div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="pt-5">
      <div class="flex justify-end">
        <button type="button" class="rounded-md border border-gray-300 bg-white py-2 px-4 text-sm font-medium text-gray-700 shadow-sm hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Cancel</button>
        <button @click="submitForm" type="submit" class="ml-3 inline-flex justify-center rounded-md border border-transparent bg-indigo-600 py-2 px-4 text-sm font-medium text-white shadow-sm hover:bg-indigo-700 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2">Save</button>
      </div>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      userId: this.$route.params.userId,
      task: {}
    }
  },
  async fetch() {
    this.task = await fetch('http://localhost:8888/api/tasks/' + this.$route.params.id)
      .then(res => res.json())
  },
  methods: {
    submitForm() {
      this.$axios.$put('http://localhost:8888/api/tasks/' + this.task.id, this.task)
      // .then(this.user = this.user)
    }
  }
}
</script>
