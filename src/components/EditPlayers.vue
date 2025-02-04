<template>
    <PlayerEditItem
        v-for="item in playersList"
        :key="item.id"
        :item="item"
        @add-life="$emit('add-life', $event)"
        @subtract-life="$emit('subtract-life', $event)"
        @change-name="$emit('change-name', item.id, $event)"
    />

    <PlayersRatings :players-list="playersList"/>
</template>

<script>
import PlayerEditItem from './PlayerEditItem.vue';
import PlayersRatings from './PlayersRatings.vue';

export default {
    name: 'LifeCounter',

    components: {
        PlayerEditItem,
        PlayersRatings,
    },

    props: {
        playersList: {
            type: Array,
            default: () => [],
        },
    },

    computed: {
        rating() {
            const places = [...this.playersList];
            
            return places.sort((a, b) => b.life - a.life);
        }
    },
}
</script>