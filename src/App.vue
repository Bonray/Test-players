<template>
    <nav class="nav">
        <button @click="changeView('CreatePlayer')">
            Создать игрока
        </button>
        <button
            :disabled="!playersList.length"
            @click="changeView('EditPlayers')"
        >
            Редактировать игрока
        </button>
    </nav>

    <h1>
        {{ title }}
    </h1>

    <CreatePlayer
        v-if="activeView === 'CreatePlayer'"
        :players-list="playersList"
        @add-player="createPlayer"
    />
    <EditPlayers
        v-else-if="activeView === 'EditPlayers'"
        :players-list="playersList"
        @add-life="changeLives($event, 'add')"
        @subtract-life="changeLives($event, 'subtract')"
        @change-name="changeName"
    />
</template>

<script>
import CreatePlayer from './components/CreatePlayer.vue'
import EditPlayers from './components/EditPlayers.vue'

export default {
    name: 'App',
    components: {
        CreatePlayer,
        EditPlayers
    },

    data() {
        return {
            playersList: [],
            activeView: 'CreatePlayer',
        }
    },

    computed: {
        title() {
            return this.activeView === 'CreatePlayer' ? 'Добавить нового игрока' : 'Редактирование игроков';
        },
    },

    methods: {
        createPlayer(player) {
            this.playersList.push(player);
        },

        changeView(view) {
            this.activeView = view;
        },

        findPlayerById(id) {
            return this.playersList.find(pl => pl.id === id);
        },

        changeLives(id, type) {
            const player = this.findPlayerById(id);

            if (player) {
                type === 'add' ? player.life++ : player.life--;
            }
        },

        changeName(id, newName) {        
            const player = this.findPlayerById(id);        

            if (player) {
                player.name = newName;
            }
        },
    },
}
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin: 60px auto;
        width: 600px;
    }

    .nav {
        display: flex;
        justify-content: center;
        gap: 10px;
    }
</style>
