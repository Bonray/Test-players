<template>
    <div class="row">
        <input v-model="name">
        <button class="button" @click.prevent="minusLife(item)">
            -
        </button>
        <span>
            {{ item.life }}
        </span>
        <button class="button" @click.prevent="plusLife(item)">
            +
        </button>
    </div>
</template>

<script>
export default {
  name: 'PlayerEditItem',

  props: {
    item: {
        type: Object,
        default: () => ({}),
    },
  },
  
  computed: {
    name: {
        get() {
            return this.item.name;
        },

        set(val) {            
            this.$emit('change-name', val);
        },
    },
  },
  
  methods: {
    plusLife(item) {
        this.$emit('add-life', item.id);
    },

    minusLife(item) {      
        if (!item.life) {
            alert('Значение не может быть меньше нуля');
            return;
        }

        this.$emit('subtract-life', item.id);
    },
  },
}
</script>

<style lang="scss">
    .row {
        display: flex;
        align-items: center;
        margin-top: 20px;

        input {
            margin-right: 12px;
            width: 100%;
            height: 24px;
        }

        .button {
          width: 24px;
          height: 24px;
          border: none;
          background-color: transparent;
          cursor: pointer;
        }
    }
</style>