<template>
    <div class="main-app-component">
        <div class="main-app-component__buttons">
            <button @click="startServer">Start</button>
            <button @click="stopServer">Stop</button>
        </div>
        <TimestampComponent :state="status" :timestamp="timestamp">

        </TimestampComponent>
    </div>
</template>

<script>
    import { ref } from '@vue/reactivity';
    import './index.scss';
    import TimestampComponent from '../TimestampComponent/index.vue'

    export default {
        name: 'MainAppComponent',
        components: { 
            TimestampComponent
        }, setup() {

            // <input type="text" v-model="status">
            
            const status = ref("offline")
            const timestamp = ref([])

            const startServer = () => {
                status.value = 'online'
                timestamp.value.push({ event : "startet server at: " + getTime()})
            }

            const stopServer = () => {
                status.value = 'offline'
                timestamp.value.push({ event: "stopped server at: " + getTime()})
            }

            function getTime() {
                var today = new Date();
                var date = today.getFullYear()+'-'+(today.getMonth()+1)+'-'+today.getDate();
                var time = today.getHours() + ":" + today.getMinutes() + ":" + today.getSeconds();
                return date + " " + time
            }

            return { status, startServer, stopServer, timestamp }
        }
    }

</script>
