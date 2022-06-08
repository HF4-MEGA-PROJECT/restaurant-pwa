<template>
  <div class="container mx-auto">
    <p class="text-4xl" style="text-align: center; padding-top: 40px">
      Bestil bord
    </p>
    <div style="text-align: -webkit-center;">
      <div style="display: block">
        <div style="text-align: -webkit-center;padding-top: 40px">
          <div class="w-full max-w-md">
            <form class="bg-white px-6 pt-10 pb-8 shadow-xl ring-1 ring-gray-900/5 sm:mx-auto sm:max-w-lg sm:rounded-lg sm:px-10 overflow-hidden" method="post" @submit.prevent="onsubmit()">
              <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="guests">
                  Oversigt
                </label>

                <div class="relative z-0 w-full mb-6 group">
                  <input
                    v-model="name"
                    type="text"
                    name="floating_name"
                    class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                    placeholder=" "
                    maxlength="40"
                    required=""
                    @keydown.enter.prevent
                  >
                  <label for="floating_name" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">Navn</label>
                </div>
                <div class="relative z-0 w-full mb-6 group">
                  <input
                    id="floating_email"
                    v-model="email"
                    type="email"
                    name="floating_email"
                    class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                    placeholder=" "
                    maxlength="60"
                    required
                    @keydown.enter.prevent
                  >
                  <label for="floating_email" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">E-mail</label>
                </div>
                <div class="grid xl:gap-6" style="width: 50%">
                  <div class="relative z-0 w-full mb-6 group">
                    <input
                      id="floating_phone"
                      v-model="phone"
                      type="tel"
                      name="floating_phone"
                      class="block py-2.5 px-0 w-full text-sm text-gray-900 bg-transparent border-0 border-b-2 border-gray-300 appearance-none dark:text-white dark:border-gray-600 dark:focus:border-blue-500 focus:outline-none focus:ring-0 focus:border-blue-600 peer"
                      placeholder=" "
                      minlength="8"
                      maxlength="8"
                      required
                      @keydown.enter.prevent
                    >
                    <label for="floating_phone" class="peer-focus:font-medium  text-sm text-gray-500 dark:text-gray-400 duration-300 transform -translate-y-6 scale-75 top-3 -z-10 origin-[0] peer-focus:left-0 peer-focus:text-blue-600 peer-focus:dark:text-blue-500 peer-placeholder-shown:scale-100 peer-placeholder-shown:translate-y-0 peer-focus:scale-75 peer-focus:-translate-y-6">Mobil</label>
                  </div>
                </div>
              </div>
              <div class="mb-4">
                <label class="block text-gray-700 text-sm font-bold mb-2" for="guests">
                  Antal gæster
                </label>
                <input
                  id="guests"
                  v-model="guestAmount"
                  class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
                  type="number"
                  placeholder="Antal gæster"
                  min="1"
                  max="15"
                  required
                  @keydown.enter.prevent
                >
              </div>
              <div class="mb-4">
                <date-picker v-model="time1" value-type="format" :disabled-date="disabledDates" @pick="joe" />
              </div>
              <div v-show="show2" class="mb-4 grid grid-cols-1 md:grid-cols-2 lg:grid-cols-2 ">
                <template v-for="time in times">
                  <Times
                    :key="time.endTime + time.startTime"
                    :available="time.available"
                    :end-time="time.endTime"
                    :start-time="time.startTime"
                    :time="time"
                    @set-time="setTime"
                  />
                </template>
              </div>
              <div v-if="isSuccess" class="success">
                Tak for din reservation, du kan nu forlade siden :)
              </div>
              <button v-show="show" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" type="submit">
                Bekræft
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DatePicker from 'vue2-datepicker'
import 'vue2-datepicker/index.css'
import axios from 'axios'
import Swal from 'sweetalert2'
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Booking',
  components: { DatePicker },
  data () {
    return {
      loading: true,
      show: true,
      show2: false,
      name: '',
      email: '',
      phone: '',
      guestAmount: '',
      formTime: '',
      time1: null,
      time2: null,
      time3: null,
      dates: [],
      times: ['2022-06-03'],
      isSuccess: false
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
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    onsubmit () {
      const data = {
        name: this.name,
        email: this.email,
        phone: this.phone,
        amount_of_people: this.guestAmount,
        time: this.formTime
      }
      axios
        .post(`/api/${'api/reserve'}`, data, {
          headers: {
            Accept: 'application/json'
          }
        })
        .then(
          (response) => {
            response.status === 201 ? this.isSuccess = true : this.isSuccess = false
            this.show = false

            Swal.fire({
              position: 'bottom-end',
              icon: 'success',
              title: 'Din reservation er modtaget',
              showConfirmButton: false,
              timer: 1500
            })
          },
          (response) => {
            console.log(response)
          }
        )
    },

    setTime (startT) {
      console.log(this.time1 + ' ' + startT)
      this.formTime = this.time1 + ' ' + startT
    },
    disabledDates (date) {
      const d = []
      for (let i = 0; i < this.dates.length; i++) {
        d.push(new Date(this.dates[i]))
      }
      return d.includes(date)
    },
    async joe (date) {
      this.show2 = 'true'
      const d = new Date(date)
      console.log(d)
      console.log(d.getFullYear(), d.getMonth() + 1, d.getDate())
      const config = {
        headers: {
          Accept: 'application/json'
        }
      }

      try {
        const res = await this.$axios.get(`/api/${'api/reserve/date/' + d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate() + '/' + 'times'}`, config)
        this.times = res.data
        console.log(this.times)
      } catch (err) {
        console.log(err)
      }
    }
  }
}
</script>

<style scoped>
</style>
