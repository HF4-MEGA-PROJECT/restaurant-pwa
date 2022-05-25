<template>
  <div :id="dish.id" class="flex col-span-1 w-full" style=" border-radius: 25px;">
    <div style="display: flex; width: inherit">
      <div class="flex px-4 w-6/24" style="width: 285px">
        <img alt="..." class="object-cover h-48 rounded" style="width: 285px" :src=" dish.photo_path">
      </div>
      <div class="block w-full">
        <div class="flex " style="border-bottom: 1px silver solid; border-radius: 0; height: fit-content; justify-content: space-between; padding-bottom: 8px;">
          <p class="text-xl">
            {{ dish.name }}
          </p>
          <p class="text-xl float-right">
            {{ dish.price }},-
          </p>
        <!--      <p>Kategori:  <a>{{ dish.category }}</a></p>-->
        </div>
        <div style="height: fit-content">
          <p> {{ dish.description }} </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: 'Dish',
  dish: 'dish',
  props: ['dish'],
  data () {
    return {
    }
  }
}
</script>

<style scoped>

</style>
