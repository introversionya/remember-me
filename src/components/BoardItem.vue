<template>
  <span :class="getBoardItemClasses" @click="select(field.id)"></span>
</template>

<script>
import { GAME_STATUS, FIELD } from '@/constans';
import { computed } from 'vue';
export default {
  name: 'BoardItem',
  props: {
    field: {
      type: Object,
      required: true,
    },
    gameStatus: {
      type: Number,
      required: false,
      default: GAME_STATUS.NONE,
    },
  },
  setup(props) {
    const getBoardItemClasses = computed(() => {
      // 'item ' + (field.value === 1 && preview ? 'item-active' : '')
      let classes = 'item '

      if (props.field.value === FIELD.FILLED && props.gameStatus === GAME_STATUS.PREVEW || props.field.clicked) {
        classes += 'active'
      }

      return classes
    })

    return {
      getBoardItemClasses
    }
  },
  methods: {
    select(id) {
      if (this.gameStatus === GAME_STATUS.STARTED) {
        this.$emit('selectField', id)
      }
    }
  }
};
</script>

<style scoped>
.item {
  position: relative;
  display: inline-block;
  width: 50px;
  height: 50px;
  background-color: #ccc;
  margin: 5px;
  cursor: pointer;
  transition: 0.4s;
  transform-style: preserve-3d;
}

.item.active {
  background-color: #42b983cc;
  transform: rotateX(180deg);
}
</style>
