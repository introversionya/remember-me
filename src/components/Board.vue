<template>
  <div class="board-wrapper">
    <div class="board">
      <BoardItem
        v-for="i in 25"
        :key="'item-' + i"
      />
    </div>

    <p class="difficult">Сложность: <strong>{{ difficult }}</strong></p>

    <button class="btn">Старт</button>
  </div>
</template>

<script>
import { ref } from 'vue';
import BoardItem from '@/components/BoardItem.vue';

export default {
  name: 'Board',

  components: {
    BoardItem,
  },

  setup() {
    const difficult = ref(3);

    return {
      difficult
    }
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
