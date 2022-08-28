<template>
  <header class="header">
    <h1>todos</h1>
    <input id="toggle-all" class="toggle-all" type="checkbox" v-model="isAll" />
    <label for="toggle-all"></label>
    <input
      class="new-todo"
      placeholder="输入任务名称-回车确认"
      autofocus
      v-model="task"
      @keydown.enter="addTask"
    />
  </header>
</template>

<script>
export default {
  props: ["list"],
  data() {
    return {
      task: "",
    };
  },
  methods: {
    addTask() {
      if (this.task.trim() === "") return alert("任务名字不能为空");
      this.$emit("add-task", this.task);
      this.task = "";
    },
  },
  computed: {
    isAll: {
      get() {
        return this.list.every((item) => item.isDone);
      },
      set(checked) {
        this.list.forEach((item) => (item.isDone = checked));
      },
    },
  },
};
</script>

<style></style>
