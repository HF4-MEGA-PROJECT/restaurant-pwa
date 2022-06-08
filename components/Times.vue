<template>
  <div class="bg-white flex col-span-1 md:col-span-1 lg:col-span-1 justify-center">
    <button type="button" class="mt-1 block px-3 py-2 rounded-md text-base font-medium text-gray-800  hover:bg-gray-200 focus:outline-none focus:bg-gray-200" @click="setTime(time.startTime)">
      {{ time.startTime }} - {{ time.endTime }}
    </button>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Time',
  time: 'time',
  props: ['time'],
  data () {
    return {
    }
  },
  methods: {
    setTime (startT) {
      this.$emit('set-time', startT)
    }
  }
}
</script>

<style scoped>

</style>
