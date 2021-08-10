<template>
  <AddTask @fnEmitNewTask="fnSaveNewTask" />

  <h3 class="todo_title" v-if="tasks_list.length > 0">Task List</h3>
  <Tasks
    v-if="tasks_list.length > 0"
    :tasks_list="tasks_list"
    @fnEmitAndSaveChangedTask="fnPutTaskOnList"
    @fnEmitDeleteTaskFromList="fnDeleteTaskFromList"
  />

  <h3 class="todo_title" v-if="tasks_list_end.length > 0">Task List End</h3>
  <Tasks
    v-if="tasks_list_end.length > 0"
    :tasks_list="tasks_list_end"
    @fnEmitAndSaveChangedTask="fnPutTaskOnList"
    @fnEmitDeleteTaskFromList="fnDeleteTaskFromEndList"
  />

  <h2 v-if="fnIsAllTaskListEmpty" class="no_task">Don´t have any task</h2>
  
</template>
<style lang="scss" scoped>
.todo_title {
  margin-top: 0.5em;
}

.no_task {
  padding: 1rem;
}
</style>

<script>
import Tasks from "@/components/Tasks";
import AddTask from "@/components/AddTask";
export default {
  name: "Todo",
  components: { Tasks, AddTask },
  data: () => ({
    tasks_list: [],
    tasks_list_end: [],
    max_id: -1,
  }),
  created() {
    const initial = [
      { id: 1, task: "Learn Vue", status: "active" },
      { id: 2, task: "Lear React", status: "end" },
    ];
    initial.forEach((data) => {
      this.max_id = this.max_id < data.id ? data.id : this.max_id;

      if (data.status === "active") this.tasks_list.push(data);
      else this.tasks_list_end.push(data);
    });
  },
  computed: {
    fnIsAllTaskListEmpty: function () {
      return this.tasks_list.length < 1 && this.tasks_list_end < 1;
    },
  },
  methods: {
    fnDeleteTaskFromList: function ({ task_id }) {
      const index = this.tasks_list.findIndex((task) => task.id === task_id);
      this.tasks_list.splice(index, 1);
    },
    fnDeleteTaskFromEndList: function ({ task_id }) {
      const index = this.tasks_list_end.findIndex(
        (task) => task.id === task_id
      );
      this.tasks_list_end.splice(index, 1);
    },

    fnSaveNewTask: function (newTaskValue) {
      this.max_id += 1;
      const newTask = { id: this.max_id, task: newTaskValue, status: "active" };
      this.tasks_list.push(newTask);
    },

    fnGetTaskByList: function ({ tasks, task_id }) {
      const index = tasks.findIndex((data) => {
        return data.id === task_id;
      });
      const task = tasks.splice(index, 1)[0];
      task.status = task.status === "active" ? "end" : "active";
      return task;
    },

    fnPutTaskOnList: function ({ task_id, task_status }) {
      if (task_status === true) {
        const task_i = this.fnGetTaskByList({
          tasks: this.tasks_list_end,
          task_id,
        });
        this.tasks_list.push(task_i);
      } else {
        const task_f = this.fnGetTaskByList({
          tasks: this.tasks_list,
          task_id,
        });
        this.tasks_list_end.push(task_f);
      }
    },
  },
};
</script>
