<template>
        <div class="timestamp-component__status">
            <p>current state: {{ state }}</p>
        </div>
    <div class="timestamp-component">
        <ul class="timestamp-component__list">
            <li v-for="time in timestamp" :key="time.event">
                [EVENT] {{ time.event }}
            </li>
        </ul>
    </div>
</template>

<script>
    import './index.scss';
    export default {
        name: 'EditPlayerComponent',
        props: {
            state: String,
            timestamp: Array
        }
    }

</script>
