<template>
  <ul class="todo-list">
    <!-- completed: 完成的类名 -->
    <li
      :class="{ completed: item.isDone }"
      v-for="item in filterdList"
      :key="item.id"
    >
      <div class="view">
        <input class="toggle" type="checkbox" v-model="item.isDone" />
        <label>{{ item.name }}</label>
        <button class="destroy" @click="delTodo(item)"></button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  props: ["list", "changeState"],
  computed: {
    filterdList() {
      switch (this.changeState) {
        case "全部":
          return this.list;
        case "未完成":
          return this.list.filter((itme) => !itme.isDone);
        case "已完成":
          return this.list.filter((itme) => itme.isDone);
        default:
          return [];
      }
    },
  },
  methods: {
    delTodo({ id }) {
      this.$emit("del-Todo", id);
    },
  },
};
</script>

<style></style>
