<template>
  <div class="todoapp">
    <!-- 在这里接收到子组件传来的值, 并为它绑定一个事件 -->
    <TodoHeader @addTodo="addTodo" :list="list"></TodoHeader>
    <!-- 接收子组件传到的id, 并绑定del事件 -->
    <TodoMain :list="filterList" @delTodo="del"></TodoMain>
    <TodoFooter
      :list="list"
      :state="state"
      @changeState="changeState"
      @clearFinished="clearFinished"
    ></TodoFooter>
  </div>
</template>

<script>
import TodoFooter from "./components/TodoFooter.vue";
import TodoHeader from "./components/TodoHeader.vue";
import TodoMain from "./components/TodoMain.vue";
export default {
  components: {
    TodoMain,
    TodoHeader,
    TodoFooter,
  },
  data() {
    const data = JSON.parse(localStorage.getItem("todo"));
    return {
      list: data || [
        { id: 100, name: "吃饭", isDone: true },
        { id: 201, name: "睡觉", isDone: false },
        { id: 103, name: "打豆豆", isDone: true },
      ],
      // 筛选的状态
      state: "all", // all 全部, finished 已完成, unfinished 未完成
    };
  },
  methods: {
    addTodo(newmsg) {
      // console.log(newmsg);
      // 接收到子元素传来的值之后, 添加到数组中
      // 给数组添加一个元素了
      this.list.unshift({ id: Date.now(), name: newmsg, isDone: false });
    },
    del(id) {
      // console.log("id:", id);
      // 既然是删除的话 那就把传过来的id给它过滤掉即可
      this.list = this.list.filter((v) => v.id !== id);
    },
    changeState(state) {
      this.state = state;
    },
    clearFinished() {
      this.list = this.list.filter((v) => v.isDone === false);
    },
  },
  // 计算属性
  computed: {
    // 基于state筛选出来的新数组
    filterList() {
      // console.log(this.state);
      switch (this.state) {
        case "all":
          // 返回所有
          return this.list;
          break;
        case "finished":
          // 返回isDone true
          return this.list.filter((v) => v.isDone === true);
          break;
        case "unfinished":
          // 返回isDone false
          return this.list.filter((v) => v.isDone === false);
          break;
      }
    },
  },
  // 添加一个侦听器, 将数据保存到本地
  watch: {
    list: {
      // 数据改变执行的逻辑
      handler() {
        // 写入缓存, 将数组转换为JSON
        localStorage.setItem("todo", JSON.stringify(this.list));
      },
      // 开启深度侦听, 因为list数组里面是对象
      deep: true,
    },
  },
};
</script>

<style></style>
