<template>
  <li :id="category.id" class="" style="padding-right: 10px; padding-left: 10px">
    <p class="text-lg cursor-pointer" @click="categoryPicker(category.id)">
      {{ category.name }}
    </p>
  </li>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Category',
  props: ['category'],
  data () {
    return {
    }
  },
  methods: {
    categoryPicker (id) {
      this.$emit('category-picker', id)
    }
  }
}
</script>

<style scoped>

</style>
