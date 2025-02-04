<template>
    <h2>Рейтинг</h2>

    <table v-if="rating.length">
        <tr
            v-for="(item, index) in rating"
            :key="item.id"
        >
            <td v-text="`${index + 1}`" />
            <td v-html="`У игрока <b>${item.name}</b> ${item.life} жизней`" />
        </tr>
    </table>

    <h3 v-else>
        Пока в рейтинге нет игроков. Добавьте нового, чтобы увидеть его в списке!
    </h3>
</template>

<script>
export default {
    name: 'PlayersRatings',

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


<style lang="scss">
    table {
        width: 100%;

        td {
            border: 1px solid #2c3e50;
        }
    }
</style>