<template>
  <form action="" class="AddTaskImpForm">
    <input type="text" class="AddTaskImpText" v-model="taskName" />
    <button class="btn_add_task" @click="fnAddNewTask">Add</button>
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data: function () {
    return {
      taskName: "",
    };
  },
  methods: {
    fnAddNewTask(event) {
      event.preventDefault();
      if (this.taskName && this.taskName.length > 0) {
        this.$emit("fnEmitNewTask", this.taskName);
      }
      this.taskName = "";
    },
  },
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/todo";
.AddTaskImpText {
  height: 2em;
  padding-left: 1em;
  padding-right: 1em;
  width: 85%;
  background-color: $slate-gray;
  color: $cultured;
  border: none;
  border-radius: 0.5em;
  margin-top: 1em;
  position: relative;
  z-index: 99;
}

.AddTaskImpForm {
  display: flex;
  width: 60%;
  position: relative;
  .btn_add_task {
    position: absolute;
    height: 2em;
    margin-top: 1em;
    width: 20%;
    right: 0;
    z-index: 9;
    border-radius: 0.5em;
    border: none;
    background-color: darken($gunmetal, 50%);
    color: darken($cultured, 25%);
    font-weight: bold;
  }
}
</style>
