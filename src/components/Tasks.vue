<template>
  <div class="task_list_container">
    <Task
      v-for="task in tasks_list"
      :task_item="task"
      :key="task.id"
      @fnEmitTaskChanged="fnSaveChangedTask"
      @fnEmitDeleteTask="fnDeleteTask"
    />
  </div>
</template>

<style lang="scss" scoped>
@import "@/assets/styles/todo";
.task_list_container {
  padding-top: 1em;
  position: relative;
  width: 60%;
  :nth-child(even).task_item {
    background-color: lighten($gunmetal, 5%);
  }
  :nth-child(odd).task_item {
    background-color: lighten($gunmetal, 10%);
  }
}
</style>
<script>
import Task from "@/components/Task";
export default {
  name: "Tasks",
  components: {
    Task,
  },
  props: {
    tasks_list: {
      default: [],
    },
  },
  computed: {
    compTaskListNotEmpty: function () {
      return this.tasks_list.length && this.tasks_list.length > 0;
    },
  },
  methods: {
    fnSaveChangedTask: function ({ task_id, task_status }) {
      this.$emit("fnEmitAndSaveChangedTask", { task_id, task_status });
    },
    fnDeleteTask: function ({ task_id }) {
      this.$emit("fnEmitDeleteTaskFromList", { task_id });
    },
  },
};
</script>
