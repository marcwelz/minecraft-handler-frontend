<template>
    <div class="edit-player-component">
        <div class="edit-player-component__online">
          <h1>Current online: {{players.length}}</h1>
        </div>
        <div class="edit-player-component__table">
          <table>
            <tr v-for="player in players" :key="player.id">
              <th>
                {{player.name}}
              </th>
              <th class="edit-player-component__table--button">
                <button @click="handleClick(player)">remove</button>
              </th>
            </tr>
          </table>
        </div>
    </div>
</template>

<script>
  import './index.scss';
  import { ref } from '@vue/reactivity';

  export default {
    name: 'EditPlayerComponent',
    props: {
      propsPlayers: Array, 
      command:Function
    },
    setup(props) {

      const players = ref([])

      for(let k = 0; k < props.propsPlayers.length; k++) {
        players.value.push(props.propsPlayers[k])
      }

      const handleClick = (slelectedPlayer) => {
        for(let i = 0; i < players.value.length; i++) {
          if(players.value[i].id === slelectedPlayer.id) {
            props.command(players.value[i].name)
            players.value.splice(i, 1)
          }
        }
      }

      return { players, handleClick }
    }
}
</script>
