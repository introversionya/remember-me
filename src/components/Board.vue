<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem
        v-for="field in fields"
        :key="'item-' + field.id"
        :field="field"
        :preview="preview"
      />
    </div>

    <p class="difficult">
      Сложность: <strong>{{ difficult }}</strong>
    </p>

    <button
      class="btn"
      @click="start"
    >
      Старт
    </button>
  </div>
</template>

<script>
import BoardItem from '@/components/BoardItem.vue';
import useGameInit from '@/components/composables/useGameInit'
import useGameStart from '@/components/composables/useGameStart'

export default {
  name: 'Board',

  components: {
    BoardItem,
  },

  setup() {

    const number = 25;

    const { difficult, fields, init } = useGameInit(number)

    const { start, preview } = useGameStart(init, fields, difficult, number)

    return {
      number,
      difficult,
      fields,
      init,
      start,
      preview
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
</style>
