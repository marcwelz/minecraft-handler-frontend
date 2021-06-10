<template>
        <div class="timestamp-component__status">
            <p>online: {{ state }}</p>
        </div>
    <div class="timestamp-component">
        <ul class="timestamp-component__list">
            <li v-for="time in timestamps" :key="time.event">
                {{ time.event }}
            </li>
        </ul>
    </div>
    <div class="timestamp-component__console-input">
        <input type="text" id="elementId" placeholder="Enter a command" v-model="search">
        <button class="timestamp-component__console-input--go-button" @click="handleCommand">Go</button>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity';
    import './index.scss';
    export default {
        name: 'EditPlayerComponent',
        props: {
            state: String,
            timestamp: Array
        }, setup(props) {

            const timestamps = ref(props.timestamp)
            const search = ref("")

            const handleCommand = () => {
                if(search.value !== '') {
                    timestamps.value.push({event: "[CONSOLE] " + search.value})

                    fetch("http://" + window.location.hostname + ":8000/server/command", {
                        method: "Post",
                        headers: {
                            "Content-Type": "application/json",
                        },
                        body: JSON.stringify({
                            command: search.value,
                        }),
                    }).then((res) => res.status === 200)

                    search.value = ""
                }
            }

            return { handleCommand, search, timestamps }
        }
    }

</script>
