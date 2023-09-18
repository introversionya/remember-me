<template>
  {{ fields }}
  <div class="board-wrapper">
    <div class="board">
      <BoardItem
        v-for="field in fields"
        :key="'item-' + field.id"
        :field="field"
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
import { onBeforeMount, ref } from 'vue';
import BoardItem from '@/components/BoardItem.vue';

export default {
  name: 'Board',

  components: {
    BoardItem,
  },

  setup() {
    let difficult = ref(3);
    let fields = ref([]);
    const number = 25;

    const init = () => {
      fields.value = [];

      for (let i = 0; i < number; i++) {
        fields.value.push({
          id: i,
          clicked: false,
          value: 0,
        });
      }
    };

    onBeforeMount(init);

    return {
      number,
      difficult,
      fields,
      init,
    };
  },

  methods: {
    start() {
      this.init();
      this.prepareGame();
    },

    prepareGame() {
      for (let i = 0; i < this.difficult; i++) {
        const index = this.rand(0, this.number - 1);

        if (this.fields[index].value !== 1) {
          this.fields[index].value = 1;
        } else {
          i--;
        }
      }
    },

    rand(min, max) {
      return Math.floor(Math.random() * (max - min)) + min;
    },
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
