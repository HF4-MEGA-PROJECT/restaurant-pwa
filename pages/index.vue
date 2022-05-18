<template>
  <div class="container mx-auto">
    <div class="grid grid-cols-1 md:grid-cols-1 lg:grid-cols-5 " style="padding: 40px">
      <div
        class="flex col-span-1 md:col-span-1 lg:col-span-2 justify-center"
        style=" border-radius: 25px; padding-bottom: 40px"
      >
        <div class="relative flex flex-col" style="max-height: 100%">
          <div
            class="relative bg-white px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10 overflow-hidden"
          >
            <div class="mx-auto max-w-md">
              <div class="divide-y divide-gray-300/50">
                <div class="space-y-6 py-8 text-base leading-7 text-gray-600">
                  <p id="topText">
                    Café Vesuvius ligger i et velbesøgt område i centrum af Odense. Det var oprindelig en vinhandler,
                    der lå her, komplet med vinkælder og showroom
                  </p>
                  <ul class="space-y-4">
                    <li class="flex items-center">
                      <svg
                        class="h-6 w-6 flex-none fill-sky-100 stroke-sky-500 stroke-2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                      >
                        <circle cx="12" cy="12" r="11" />
                        <path d="m8 13 2.165 2.165a1 1 0 0 0 1.521-.126L16 9" fill="none" />
                      </svg>
                      <p id="dot1" class="ml-4">
                        I sommerhalvåret er der mulighed for at spise udendørs, og der stilles tæpper til rådighed.
                      </p>
                    </li>
                    <li class="flex items-center">
                      <svg
                        class="h-6 w-6 flex-none fill-sky-100 stroke-sky-500 stroke-2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                      >
                        <circle cx="12" cy="12" r="11" />
                        <path d="m8 13 2.165 2.165a1 1 0 0 0 1.521-.126L16 9" fill="none" />
                      </svg>
                      <p id="dot2" class="ml-4">
                        Friske ingredienser direkte fra vores lokale leverandøre
                      </p>
                    </li>
                    <li class="flex items-center">
                      <svg
                        class="h-6 w-6 flex-none fill-sky-100 stroke-sky-500 stroke-2"
                        stroke-linecap="round"
                        stroke-linejoin="round"
                      >
                        <circle cx="12" cy="12" r="11" />
                        <path d="m8 13 2.165 2.165a1 1 0 0 0 1.521-.126L16 9" fill="none" />
                      </svg>
                      <p id="dot3" class="ml-4">
                        Perfekt sted at nyde din eftermiddag
                      </p>
                    </li>
                  </ul>
                </div>
                <div class="pt-8 text-base font-semibold leading-7">
                  <p class="text-gray-900">
                    Mandag til Fredag:
                    <a id="weekDay">10 - 20</a>
                  </p>
                  <p class="text-gray-900">
                    Lørdag til søndag:
                    <a id="weekEnd">10 - 18</a>
                  </p>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="flex col-span-1 md:col-span-1 lg:col-span-3">
        <div class="flex flex-wrap justify-center">
          <div class="w-6/24 px-4">
            <img
              alt="..."
              class="shadow rounded max-w-full h-auto align-middle border-none"
              src="~/assets/images/photo-1.jpg"
            >
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',

  async created () {
    const data = (await this.$axios.get('https://restaurant-backend.binau.dev/api/setting')).data
    console.log(data)
  }
})

</script>

<style>
* {
  border-radius: 5px;
}
</style>
