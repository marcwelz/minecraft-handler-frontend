<template>
    <HeaderComponent/>
  <div class="app">
    <div class="main-app">
      <div class="main-app__setting">
        <button class="main-app__setting--button" @click="changeSettings"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path fill="currentColor" d="M19.43 12.98c.04-.32.07-.64.07-.98s-.03-.66-.07-.98l2.11-1.65c.19-.15.24-.42.12-.64l-2-3.46c-.12-.22-.39-.3-.61-.22l-2.49 1c-.52-.4-1.08-.73-1.69-.98l-.38-2.65C14.46 2.18 14.25 2 14 2h-4c-.25 0-.46.18-.49.42l-.38 2.65c-.61.25-1.17.59-1.69.98l-2.49-1c-.23-.09-.49 0-.61.22l-2 3.46c-.13.22-.07.49.12.64l2.11 1.65c-.04.32-.07.65-.07.98s.03.66.07.98l-2.11 1.65c-.19.15-.24.42-.12.64l2 3.46c.12.22.39.3.61.22l2.49-1c.52.4 1.08.73 1.69.98l.38 2.65c.03.24.24.42.49.42h4c.25 0 .46-.18.49-.42l.38-2.65c.61-.25 1.17-.59 1.69-.98l2.49 1c.23.09.49 0 .61-.22l2-3.46c.12-.22.07-.49-.12-.64l-2.11-1.65zM12 15.5c-1.93 0-3.5-1.57-3.5-3.5s1.57-3.5 3.5-3.5 3.5 1.57 3.5 3.5-1.57 3.5-3.5 3.5z"/></svg></button>
      </div>
      <div class="main-app__buttons">
            <button class="main-app__buttons--start" @click="startServer">start</button>
            <button class="main-app__buttons--stop" @click="stopServer">Stop</button>
        </div>
    <TimestampComponent :state="status" :timestamp="timestamp" />
    </div>
    <EditPlayerComponent :propsPlayers="propsPlayers" :command="getCommands"/>
  </div>
    <div class="footer">
      ©copyright 2021 Welz Marc
    </div>
    <axa-modal>
      <SettingsComponent />
    </axa-modal>
</template>

<script>
import '@axa-ch/modal'
import HeaderComponent from './components/HeaderComponent/index.vue'
import EditPlayerComponent from './components/EditPlayerComponent/index.vue'
import TimestampComponent from './components/TimestampComponent/index.vue'
import SettingsComponent from './components/SettingsComponent/index.vue'
import { ref } from '@vue/reactivity';
import './App.scss'

export default {
  name: 'App',
  components: {
    HeaderComponent,
    TimestampComponent,
    EditPlayerComponent,
    SettingsComponent
  },
  setup() {

    const propsPlayers = ref([
      {id: 1, name: 'Minecrafter2028'}, {id: 2, name: 'Milchmaa'}, {id: 3, name: 'DragonBlood'}, {id: 4, name: 'HansWurst69'}, { id: 5, name: 'Bubii'}, 
      { id: 6, name: 'Recker23'}, { id: 7, name: 'InformatikerEFZ'}, { id: 8, name: 'Erazer'}, { id: 9, name: 'Dansent'}, { id: 10, name: 'Axo'}, { id: 11, name: 'ZeferiaFOX'},
      { id: 11, name: 'deathbear50'}, { id: 12, name: 'Bohler'}, { id: 13, name: 'Farmer37'}, { id: 14, name: 'vodka-pur'}, { id: 15, name: 'zigiraucher'}, { id: 16, name: 'Hotrox'},
      { id: 17, name: 'Bumeli'}, { id: 18, name: 'Joel2'}
    ])

    const timestamp = ref([])
    const status = ref(false)

    const getCommands = (command) => {
      timestamp.value.push({ event : "[CONSOLE] /kick " + command })
      timestamp.value.push({ event : "[SERVER] " + command + " got kicked from the server" })
    }

    const changeSettings = () => {
      // openSettings.value = !openSettings.value
      document.getElementsByTagName("axa-modal")[0].setAttribute("open", true)
    }

    const startServer = () => {
      fetch('http://192.168.1.232:8000/server/start', {
           method: "get",
           headers: {
            'Content-Type': 'application/json',
          },
        })
      timestamp.value.push({ event : "[EVENT] startet server at: " + getTime()})
      updateStatus()
    }

    const stopServer = () => {
      fetch('http://192.168.1.232:8000/server/stop', {
           method: "get",
           headers: {
            'Content-Type': 'application/json',
          },
        })
      timestamp.value.push({ event: "[EVENT] stopped server at: " + getTime()})
      updateStatus()
    }

    function getTime() {
      var today = new Date();
      var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
      var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
      return date + " " + time
    }

    function updateStatus() {
      fetch('http://192.168.1.232:8000/server/status', {
           method: "get",
           headers: {
            'Content-Type': 'application/json',
          },
        })
        .then(res => res.json())
        .then((data) => {
          status.value = data.status
        })
    }

    updateStatus()

    return { propsPlayers, status, startServer, stopServer, timestamp, getCommands, changeSettings }
  }
}
</script>
