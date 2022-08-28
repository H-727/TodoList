<template>
  <div>
    <todo-header @add-task="addTask" :list="list" />
    <todo-main :list="list" @del-Todo="delTodo" :changeState="state" />
    <todo-footer @change-state="changeState" @clear-done="clearDone" />
  </div>
</template>

<script>
import TodoHeader from "@/components/TodoHeader.vue";
import TodoMain from "@/components/TodoMain.vue";
import TodoFooter from "@/components/TodoFooter.vue";
import "./styles/base.css";
import "./styles/index.css";
import { v4 as uuidv4 } from "uuid";
export default {
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter,
  },
  data() {
    return {
      list: JSON.parse(localStorage.getItem("token")) || [],
      state: "全部",
    };
  },
  methods: {
    delTodo(id) {
      this.list = this.list.filter((item) => item.id !== id);
    },
    addTask(task) {
      const obj = {};
      obj.id = uuidv4();
      obj.isDone = false;
      obj.name = task;
      this.list.push(obj);
    },
    changeState(state) {
      this.state = state;
      console.log(this.state);
    },
    clearDone() {
      this.list = this.list.filter((item) => !item.isDone);
      alert("清除成功");
    },
    saveTodo(newList) {
      window.localStorage.setItem("token", JSON.stringify(newList));
    },
  },
  watch: {
    list: {
      deep: true,
      immediate: true,
      handler: "saveTodo",
    },
  },
};
</script>

<style></style>
