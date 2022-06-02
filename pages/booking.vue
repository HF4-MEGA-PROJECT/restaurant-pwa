<template>
  <div class="container mx-auto">
    <p class="text-4xl" style="text-align: center; padding-top: 40px">
      Bestil bord
    </p>
    <div style="text-align: -webkit-center;">
      <div style="display: block">
        <div style="text-align: -webkit-center;padding-top: 40px">
          <div class="w-full max-w-md">
            <form class="bg-white px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10 overflow-hidden">
              <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="guests">
                  Antal gæster
                </label>
                <input
                  id="guests"
                  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                  type="text"
                  placeholder="Antal gæster"
                  required
                >
              </div>
              <div class="mb-4">
                s
              </div>
              <div class="mb-4">
                s
              </div>
              <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="guests">
                  Oversigt
                </label>

                <div class="relative z-0 w-full mb-6 group">
                  <input type="text" name="floating_name" class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer" placeholder=" " required="">
                  <label for="floating_name" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">Navn</label>
                </div>
                <div class="relative z-0 w-full mb-6 group">
                  <input
                    id="floating_email"
                    type="email"
                    name="floating_email"
                    class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                    placeholder=" "
                    required=""
                  >
                  <label for="floating_email" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">E-mail</label>
                </div>
                <div class="grid xl:gap-6" style="width: 50%">
                  <div class="relative z-0 w-full mb-6 group">
                    <input
                      id="floating_phone"
                      type="tel"
                      pattern="[0-9]{3}-[0-9]{3}-[0-9]{4}"
                      name="floating_phone"
                      class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                      placeholder=" "
                      required=""
                    >
                    <label for="floating_phone" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">Mobil</label>
                  </div>
                </div>
              </div>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Booking',
  data () {
    return {
      dates: [],
      times: []
    }
  },
  async created () {
    const config = {
      headers: {
        Accept: 'application/json'
      }
    }

    try {
      const res = await this.$axios.get(`/api/${'api/reserve/dates'}`, config)
      this.dates = res.data.unavailable_dates
      console.log(this.dates)
    } catch (err) {
      console.log(err)
    }
  }
}
</script>

<style scoped>
</style>
