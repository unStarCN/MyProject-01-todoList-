<template>
  <header class="header">
    <h1>todos</h1>
    <input
      v-model="isCheckAll"
      id="toggle-all"
      class="toggle-all"
      type="checkbox"
    />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model.trim="msg"
      @keyup.enter="addTodo"
    />
  </header>
</template>

<script>
export default {
  data() {
    return {
      msg: "",
    };
  },
  methods: {
    addTodo() {
      // console.log(this.msg);
      // 我们在这里输入的内容需要传到父组件vue那里去, 通过$emit()方法
      if (this.msg) {
        this.$emit("addTodo", this.msg);
      }
      // console.log(this.msg);
      this.msg = "";
    },
  },
  props: {
    list: {
      type: Array,
    },
  },
  // 添加计算属性
  computed: {
    // 基于list 是否全部isDone true 决定是否勾选全选
    isCheckAll: {
      get() {
        if (this.list.length === 0) {
          return false;
        }
        return this.list.every((v) => v.isDone === true);
      },
      set(value) {
        // console.log(value);
        this.list.forEach((v) => (v.isDone = value));
      },
    },
  },
};
</script>
