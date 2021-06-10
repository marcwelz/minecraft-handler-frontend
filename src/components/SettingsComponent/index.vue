<template>
    <div class="settings-container">
        <h1>Settings</h1>
        <form>
            <div class="settings-container__setting">
                <label for="world-name">World-name </label>
                <input type="text" id="world-name" v-model="worldname" :placeholder="worldname"/><br/>
            </div>
            <div class="settings-container__setting">
                <label for="max-player">Max Players </label>
                <input type="text" id="max-player" v-model="maxplayers" :placeholder="maxplayers"/><br/>
            </div>
            <div class="settings-container__setting">
                <label for="max-player">Description </label>
                <input type="text" id="max-player" v-model="motd" :placeholder="motd"/><br/>
            </div>
            <div class="settings-container__setting">
                <label for="gamemode">gamemode </label>
                <select name="gamemode" id="gamemode" v-model="gamemode">
                    <option value="creative" id="creative">creative</option>
                    <option value="survival" id="survival">survival</option>
                    <option value="hardcore" id="hardcore">hardcore</option>
                </select><br/>
            </div>
            <div class="settings-container__setting">
                <label for="pvp">pvp </label>
                <input type="checkbox" id="pvp" v-model="pvp"/><br/>
            </div>
            <button @click="handleSetting">apply changes</button>
        </form>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity';
import './index.scss';
export default {
    name: "SettingsComponent",
    setup() {

        const worldname = ref("")
        const maxplayers = ref("")
        const motd = ref("")
        const gamemode = ref("")
        const pvp = ref(false)
        
        function getServerSettings() {
            fetch('http://192.168.1.232:8000/server/settings/get', {
                method: "get",
                headers: {
                    'Content-Type': 'application/json',
                },
            })
            .then(res => res.json())
            .then((data) => {
                gamemode.value = data.gamemode
                pvp.value = data.pvp
                worldname.value = data.worldname
                maxplayers.value = data.maxplayers
                motd.value = data.motd
            })
        }

        getServerSettings();

        const handleSetting = () => {
            if(worldname.value !== "" && maxplayers.value !== "") {
                fetch("http://192.168.1.232:8000/server/settings", {
                    method: "Post",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        settings: [gamemode.value, pvp.value, worldname.value, maxplayers.value, motd.value]
                    }),
                }).then((res) => res.status === 200)
            }
        }

        return { handleSetting, worldname, maxplayers, motd, gamemode, pvp }
    }
}
</script>
