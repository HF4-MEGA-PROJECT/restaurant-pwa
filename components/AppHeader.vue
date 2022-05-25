<template>
  <div>
    <div>
      <nav class="bg-white shadow-xl">
        <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
          <div class="flex items-center justify-between h-16">
            <div class="flex items-center">
              <div class="flex-shrink-0">
                <img alt="Cafe logo" class="w-16 w-16" src="~/assets/images/Cafe_logo_png_fix.png">
              </div>
              <div class="hidden md:block">
                <div class="ml-10 flex items-baseline">
                  <NuxtLink
                    class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-200 focus:outline-none focus:bg-gray-200"
                    to="/"
                  >
                    Velkommen
                  </NuxtLink>
                  <NuxtLink
                    class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-200 focus:outline-none focus:bg-gray-200"
                    to="/menu"
                  >
                    Menu
                  </NuxtLink>
                  <NuxtLink
                    class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-200 focus:outline-none focus:bg-gray-200"
                    to="/"
                  >
                    Bestil bord
                  </NuxtLink>
                </div>
              </div>
            </div>
            <div class="-mr-2 flex md:hidden" style="margin: 8px">
              <!-- Mobile menu button -->
              <button
                class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-white hover:bg-gray-700 focus:outline-none focus:bg-gray-700 focus:text-white"
                @click="toggle"
              >
                <svg
                  :class="[isOpen ? 'hidden' : 'block', 'h-6 w-6']"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    d="M4 6h16M4 12h16M4 18h16"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                  />
                </svg>
                <svg
                  :class="[isOpen ? 'block' : 'hidden', 'h-6 w-6']"
                  fill="none"
                  stroke="currentColor"
                  viewBox="0 0 24 24"
                >
                  <path
                    d="M6 18L18 6M6 6l12 12"
                    stroke-linecap="round"
                    stroke-linejoin="round"
                    stroke-width="2"
                  />
                </svg>
              </button>
            </div>
          </div>
        </div>
        <div :class="[isOpen ? '' : 'hidden', 'md:hidden']">
          <div class="px-2 pt-2 pb-3 sm:px-3">
            <NuxtLink
              class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-300 focus:outline-none focus:bg-gray-300"
              to="/"
            >
              Velkommen
            </NuxtLink>
            <NuxtLink
              class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-300 focus:outline-none focus:bg-gray-300"
              to="/menu"
            >
              Menu
            </NuxtLink>
            <NuxtLink
              class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-300 focus:outline-none focus:bg-gray-300"
              to="/"
            >
              Bestil bord
            </NuxtLink>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      isOpen: false
    }
  },
  methods: {
    toggle () {
      this.isOpen = !this.isOpen
    }
  }
}
</script>
