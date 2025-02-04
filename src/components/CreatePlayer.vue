<template>
    <div class="row">
        <input id="name" type="text" v-model="playerName" placeholder="Имя"/>
        <input id="life" type="number" v-model="playerLife" placeholder="Жизней" min="1" />
        <button type="button" @click="createPlayer">Создать</button>
    </div>
</template>


<script>
export default {
  name: 'CreatePlayer',
  
  data () {
    return {
      playerName: '',
      playerLife: ''
    };
  },
  
  methods: {
    createPlayer() {
        if(!this.playerName) {
            alert('Укажите имя');
            return;
        }

        if(!this.playerLife) {
            alert('Укажите количество жизней');
            return;
        }

        if(this.playerLife <= 0) {
            alert('Значение не может быть меньше нуля');
            return;
        }

        this.$emit('add-player', {
            id: Date.now().toString(36) + Math.random().toString(36).slice(2),
            name: this.playerName,
            life: this.playerLife,
        });
        
        this.playerName = '';
        this.playerLife = '';
    }
  },
}
</script>

<style lang="scss">
    .row {
        display: flex;
        margin-top: 20px;

        input {
            margin-right: 12px;
            width: 100%;
            height: 24px;
        }

        button {
            width: 70px;
        }
    }

    #life {
        width: 70px;
    }
</style>
