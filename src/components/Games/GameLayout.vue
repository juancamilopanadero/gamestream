<script setup>
import { useSlots, ref } from 'vue';
import SharedSearch from '../Shared/SharedSearch.vue';
const slots = useSlots()
const searchInput = ref('')
const emit = defineEmits(['setGameView'])
const { games } = defineProps({
  games:{
    type: Array,
    required: true
  }
})

const onSearch = () =>{
  if (searchInput.value.toLowerCase().trim()===''){
    emit('setGameView', games)
    return 
  }
  console.log(games)
  const filteredGames = games.filter((game) => {
    return game.title.toLowerCase().includes(searchInput.value.toLowerCase())
  })
  console.log(filteredGames)
  emit('setGameView', filteredGames)

}

</script>

<template>
  <section>

    <slot name="title" />
   
    <h2 v-if="slots.title === undefined">Recent games</h2>
  

    <div class="game-layout">
      <SharedSearch @search="onSearch" v-model="searchInput" class="my-class" id="search-form"/>
      <slot />

    </div>
  </section>
</template>

<style scoped>
.game-layout {
  display: grid;
  gap: 2rem;
  margin: 1rem auto;
  max-width: 90%;
}
</style>
