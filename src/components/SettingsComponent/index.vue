<template>
    <div class="settings-container">
        <h1>Settings</h1>
        <form>
            <div class="settings-container__setting">
                <label for="world-name">World-name </label>
                <input type="text" id="world-name" /><br/>
            </div>
            <div class="settings-container__setting">
                <label for="max-player">Max Players </label>
                <input type="text" id="max-player" /><br/>
            </div>
            <div class="settings-container__setting">
                <label for="gamemode">gamemode </label>
                <select name="gamemode" id="gamemode">
                    <option value="creative">creative</option>
                    <option value="survival" selected>survival</option>
                    <option vlaue="hardcore">hardroce</option>
                </select><br/>
            </div>
            <div class="settings-container__setting">
                <label for="whitelist">whitelist </label>
                <input type="checkbox" id="whitelist" /><br/>
            </div>
        </form>
    </div>
</template>

<script>
import './index.scss';
export default {
    name: "SettingsComponent"
}
</script>
