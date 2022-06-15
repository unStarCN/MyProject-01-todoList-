<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li :class="{ completed: item.isDone }" v-for="item in list" :key="item.id">
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone" />
        <label>{{ item.name }}</label>
        <button class="destroy" @click="del(item.id)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: "TodoMain",
  props: {
    // list属性
    list: {
      // 类型是数组
      type: Array,
    },
  },
  methods: {
    del(id) {
      // 获取到当前的id了, 传到父组件那里去
      // console.log(id);
      this.$emit("delTodo", id);
    },
  },
};
</script>
