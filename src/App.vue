<template>
    <HeaderComponent/>
  <div class="app">
    <div class="main-app">
      <div class="main-app__buttons">
            <button class="main-app__buttons--start" @click="startServer">Start</button>
            <button class="main-app__buttons--stop" @click="stopServer">Stop</button>
        </div>
    <TimestampComponent :state="status" :timestamp="timestamp" />
    </div>
    <EditPlayerComponent :propsPlayers="propsPlayers" :command="getCommands"/>
  </div>
    <div class="footer">
      ©copyright 2021 Welz Marc
    </div>
</template>

<script>
import HeaderComponent from './components/HeaderComponent/index.vue'
import EditPlayerComponent from './components/EditPlayerComponent/index.vue'
import TimestampComponent from './components/TimestampComponent/index.vue'
import { ref } from '@vue/reactivity';
import './App.scss'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    TimestampComponent,
    EditPlayerComponent
  },
  setup() {

    const propsPlayers = ref([
      {id: 1, name: 'Minecrafter2028'}, {id: 2, name: 'Milchmaa'}, {id: 3, name: 'DragonBlood'}, {id: 4, name: 'HansWurst69'}, { id: 5, name: 'Bubii'}, 
      { id: 6, name: 'Recker23'}, { id: 7, name: 'InformatikerEFZ'}, { id: 8, name: 'Erazer'}, { id: 9, name: 'Dansent'}, { id: 10, name: 'Axo'}, { id: 11, name: 'ZeferiaFOX'},
      { id: 11, name: 'deathbear50'}, { id: 12, name: 'Bohler'}, { id: 13, name: 'Farmer37'}, { id: 14, name: 'vodka-pur'}, { id: 15, name: 'zigiraucher'}, { id: 16, name: 'Hotrox'},
      { id: 17, name: 'Bumeli'}, { id: 18, name: 'Joel2'}
    ])

    const status = ref("offline")
    const timestamp = ref([])

    const getCommands = (command) => {
      timestamp.value.push({ event : "[CONSOLE] /kick " + command })
      timestamp.value.push({ event : "[SERVER] " + command + " got kicked from the server" })
    }

    const startServer = () => {
      status.value = 'online'
      timestamp.value.push({ event : "[EVENT] startet server at: " + getTime()})
    }

    const stopServer = () => {
      status.value = 'offline'
      timestamp.value.push({ event: "[EVENT] stopped server at: " + getTime()})
    }

    function getTime() {
      var today = new Date();
      var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
      var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      return date + " " + time
    }

    // only temporary
    for(let i = 0; i < 20; i++) {
      i % 2 ? timestamp.value.push({ event: "[EVENT] stopped server at: " + getTime()}) : timestamp.value.push({ event : "[EVENT] startet server at: " + getTime()})
    }

    return { propsPlayers, status, startServer, stopServer, timestamp, getCommands }
  }
}
</script>
