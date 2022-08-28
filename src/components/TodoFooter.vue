<template>
  <footer class="footer">
    <span class="todo-count">剩余<strong>数量值</strong></span>
    <ul class="filters">
      <li v-for="item in lis" :key="item.id">
        <a
          :class="{ selected: flag === item.id }"
          @click="[(flag = item.id), $emit('change-state', item.name)]"
          href="javascript:;"
          >{{ item.name }}</a
        >
      </li>
    </ul>
    <button class="clear-completed">清除已完成</button>
  </footer>
</template>

<script>
import { v4 as uuidv4 } from "uuid";
export default {
  data() {
    const lis = [
      {
        id: uuidv4(),
        name: "全部",
      },
      {
        id: uuidv4(),
        name: "已完成",
      },
      {
        id: uuidv4(),
        name: "未完成",
      },
    ];
    return {
      flag: lis[0].id,
      lis,
    };
  },
};
</script>

<style></style>
