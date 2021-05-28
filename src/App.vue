<template>
    <HeaderComponent/>
  <div class="app">
    <MainAppComponent/>
    <EditPlayerComponent :propsPlayers="propsPlayers"/>
  </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent/index.vue'
import EditPlayerComponent from './components/EditPlayerComponent/index.vue'
import MainAppComponent from './components/MainAppComponent/index.vue'
import { ref } from '@vue/reactivity';
import './App.scss'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    MainAppComponent,
    EditPlayerComponent
  },
  setup() {
    const propsPlayers = ref([
      {id: 1, name: 'Minecrafter2028'}, {id: 2, name: 'Milchmaa'}, {id: 3, name: 'DragonBlood'}, {id: 4, name: 'HansWurst69'}, { id: 5, name: 'Bubii'}, 
      { id: 6, name: 'Recker23'}, { id: 7, name: 'InformatikerEFZ'}, { id: 8, name: 'Erazer'}, { id: 9, name: 'Dansent'}, { id: 10, name: 'Axo'}, { id: 11, name: 'ZeferiaFOX'},
      { id: 11, name: 'deathbear50'}, { id: 12, name: 'Bohler'}, { id: 13, name: 'Farmer37'}, { id: 14, name: 'vodka-pur'}, { id: 15, name: 'zigiraucher'}, { id: 16, name: 'Hotrox'},
      { id: 17, name: 'Bumeli'}, { id: 18, name: 'Joel2'}
    ])

    return { propsPlayers }
  }
}
</script>
