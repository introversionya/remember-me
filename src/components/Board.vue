<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem
        v-for="field in fields"
        :key="'item-' + field.id"
        :field="field"
        :game-status="gameStatus"
        @selectField="selectField($event)"
      />
    </div>

    <p class="difficult">
      Сложность: <strong>{{ difficult }}</strong>
    </p>

    <button
      class="btn"
      @click="start"
      :disabled="!canStartGame"
    >
      Старт
    </button>
  </div>
</template>

<script>
import { ref } from 'vue'
import BoardItem from '@/components/BoardItem.vue';
import useGameInit from '@/components/composables/useGameInit'
import useGameStart from '@/components/composables/useGameStart'
import useGameProcess from '@/components/composables/useGameProcess'
import { GAME_STATUS } from '@/constans'

export default {
  name: 'Board',

  components: {
    BoardItem,
  },

  setup() {

    const gameStatus = ref(GAME_STATUS.NONE)

    const number = 25;

    const { difficult, fields, init } = useGameInit(number)

    const { start, canStartGame } = useGameStart(init, fields, difficult, number, gameStatus)

    const { selectField } = useGameProcess(fields)

    return {
      number,
      difficult,
      fields,
      init,
      start,
      gameStatus,
      canStartGame,
      selectField
    };
  },
};
</script>

<style scoped>
.board-wrapper {
  margin-bottom: 100px;
}
.board {
  width: 300px;
  background-color: #eee;
  margin: 0 auto;
}
.btn {
  background-color: #42b983cc;
  color: white;
  border: none;
  border-radius: 2px;
  padding: 10px 30px;
  margin: 10px 0;
  cursor: pointer;
  outline: none;
}
.btn:hover {
  background-color: #42b983;
}

.btn:disabled {
  opacity: 0.5;
  cursor: default;
}
</style>
