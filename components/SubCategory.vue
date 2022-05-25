<template>
  <div v-if="category_dishes.length > 0">
    <span class="text-3xl border-b w-full flex text-center justify-center items-center my-8">
      {{ subcategory.name }}
    </span>
    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
      <template v-for="dish in dishes">
        <Dish
          v-if="dish.category_id === subcategory.id"
          :key="dish.id"
          :dish="dish"
        />
      </template>
      <template v-for="_subcategory in subcategories">
        <sub-category :key="_subcategory.id" :subcategory="_subcategory" :dishes="dishes" :categories="categories" />
      </template>
    </div>
  </div>
</template>

<script>
export default {
  name: 'SubCategory',
  props: ['subcategory', 'dishes', 'categories'],
  data () {
    return {}
  },
  computed: {
    subcategories () {
      const subcategories = []
      this.categories.forEach((category) => {
        if (category.category_id === this.subcategory.id) {
          subcategories.push(category)
        }
      })

      return subcategories
    },
    category_dishes () {
      const categoryDishes = []
      this.dishes.forEach((dish) => {
        if (dish.category_id === this.subcategory.id) {
          categoryDishes.push(dish)
        }
      })

      return categoryDishes
    }
  }
}
</script>

<style scoped>

</style>
