<template>
  <footer class="footer">
    <span class="todo-count"
      >剩余<strong>{{ spTodos }}</strong></span
    >
    <ul class="filters">
      <li>
        <a
          :class="{ selected: state === 'all' }"
          @click="$emit('changeState', 'all')"
          href="javascript:;"
          >全部</a
        >
      </li>
      <li>
        <a
          :class="{ selected: state === 'unfinished' }"
          @click="$emit('changeState', 'unfinished')"
          href="javascript:;"
          >未完成</a
        >
      </li>
      <li>
        <a
          :class="{ selected: state === 'finished' }"
          @click="$emit('changeState', 'finished')"
          href="javascript:;"
          >已完成</a
        >
      </li>
    </ul>
    <button class="clear-completed" @click="$emit('clearFinished')">
      清除已完成
    </button>
  </footer>
</template>

<script>
export default {
  props: {
    // 接收list属性
    list: {
      type: Array,
    },
    state: {
      type: String,
    },
  },
  // 计算属性
  computed: {
    // 剩余的todo isDone false
    spTodos() {
      // 基于list计算出结果
      // 简化写法
      return this.list.filter((v) => v.isDone === false).length;
    },
  },
};
</script>
