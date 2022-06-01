<template>
  <div class="container mx-auto">
    <p class="text-4xl" style="text-align: center; padding-top: 40px">
      Vores menu
    </p>
    <div class="">
      <ul class="" style="display: flex; justify-content: center; padding-top: 20px">
        <template v-for="category in categories">
          <Category
            v-if="category.category_id === null"
            :key="category.id"
            :category="category"
            :class="{'font-bold': currentCategory === category.id}"
            @category-picker="categoryPicker"
          />
        </template>
      </ul>
    </div>
    <div class="flex flex-col" style="padding: 40px">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
        <template v-for="dish in dishes">
          <Dish
            v-if="dish.category_id === currentCategory"
            :key="dish.id"
            :dish="dish"
          />
        </template>
      </div>
      <template v-for="subcategory in subcategories">
        <sub-category :key="subcategory.id" :subcategory="subcategory" :dishes="dishes" :categories="categories" />
      </template>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'

export default Vue.extend({
  name: 'MenuPage',
  data () {
    return {
      currentCategory: 1,
      dishes: [],
      categories: []
    }
  },

  computed: {
    subcategories () {
      const subcategories = []
      this.categories.forEach((category) => {
        if (category.category_id === this.currentCategory) {
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
  },

  async created () {
    const config = {
      headers: {
        Accept: 'application/json'
      }
    }
    try {
      const res = await this.$axios.get(`/api/${'api/menu'}`, config)
      console.log(res.data.products)
      this.dishes = res.data.products
    } catch (err) {
      console.log(err)
    }

    try {
      const res = await this.$axios.get(`/api/${'api/menu'}`, config)
      console.log(res.data.categories)
      this.categories = res.data.categories
      this.currentCategory = this.categories.find((category) => {
        return category.category_id === null
      }).id
    } catch (err) {
      console.log(err)
    }
  },
  methods: {
    categoryPicker (selected) {
      this.currentCategory = selected
    }
  }
})
</script>
