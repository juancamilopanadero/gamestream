<script setup>
import LayoutHero from './components/Layout/LayoutHero.vue';
import GameCard from './components/Games/GameCard.vue';
import GameLayout from './components/Games/GameLayout.vue';
import { onMounted, reactive, ref } from 'vue';
import GameModal from './components/Games/GameModal.vue';
import { useFetch } from './composables/useFetch';
import SharedLoader from './components/Shared/SharedLoader.vue';
const API_URL = "https://gamestreamapi.herokuapp.com/api/games"
const gamesView = ref([])
const {state} = useFetch(API_URL, (json)=>{
  gamesView.value = json

})

const setGameView = (filteredGames) => {
  gamesView.value = filteredGames
}

</script>

<template>
  <LayoutHero />
  
  
  <main>
    <SharedLoader v-if=" state.isLoading"/>
    <GameLayout v-else :games="state.data" @set-game-view="setGameView">
    
    <GameCard v-for="game in gamesView" :key="game.title" :game="game"/>

  </GameLayout>
  <Teleport to="body"/>
  <GameModal/>
  </main>
</template>

<style scoped>
main {
  padding: 2rem;
}
</style>
