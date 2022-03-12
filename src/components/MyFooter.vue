<template>
  <div class="todo-footer" v-show="total">
    <label>
      <input type="checkbox" v-model="isAll" />
    </label>
    <span>
      <span>已完成{{ doneTotal }}</span> / 全部{{ total }}
    </span>
    <button class="btn btn-danger" @click="clearAll">清除已完成任务</button>
  </div>
</template>

<script>
export default {
  name: "MyFooter",
  props: ["todos", "checkAllTodo", "clearAllTodo"], //注意冒号
  computed: {
    //总数
    total() {
      return this.todos.length;
    },
    doneTotal() {
      //条件统计
      return this.todos.filter((todo) => todo.done === true).length;
      // return this.todos.reduce((pre, todo) => pre + (todo.done ? 1 : 0), 0);
      //todo.done 是否为真？ 为真1为假0 条件，统计，实际：递归
    },

    isAll: {
      get() {
        return this.doneTotal === this.total && this.total > 0;//绑定check框，在完成总数相等且总数>0时返回真
      },
      set(value) {
        this.checkAllTodo(value);
      },
    },
  },
  methods: {
    clearAll() {
      this.clearAllTodo();
    },
  },
};
</script>

<style scoped>
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>