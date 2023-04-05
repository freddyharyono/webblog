<template>
  <div class="home">
    <h1>home</h1>
    <input type="text" v-model="search">
    <p>search term - {{ search }}</p>
    <div v-for="name in matchingNames" :key="name">{{ name }}</div>
    <button @click="handleClick">click</button>
  </div>
</template>

<script>
import { computed, reactive, ref, watch, watchEffect } from 'vue'

export default {
  name: 'HomeView',
  setup() {
    const search = ref('')
    const names = ref(['Fauzi', 'Andika', 'Salam'])

    const stopwatch = watch(search, () => {
      console.log('watch function ran')
    })

    const stopeffect = watchEffect(() => {
      console.log('watcheffect function ran', search.value)
    })

    const matchingNames = computed(() => {
      return names.value.filter((name) => name.includes(search.value))
    })

    const handleClick = () => {
      stopwatch()
      stopeffect()
    }

    return { names, search, matchingNames, handleClick }
  }
}
</script>
