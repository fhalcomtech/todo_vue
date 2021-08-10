<template>
  <div :class="'task_item task_item_' + isCheckedOn" :id="task_item.id">
    <span class="task_id"
      ><span class="delete_task" @click="fnEmitDeleteTask">x</span
      >{{ task_item.id }}</span
    >
    <span class="task_task">{{ task_item.task }}</span>
    <span class="task_status">
      <input
        type="checkbox"
        :id="'task_check_' + task_item.id"
        class="task_item_check"
        v-model="checked"
        @change="fnEmitTaskChanged"
      />
      <label
        :for="'task_check_' + task_item.id"
        :value="task_item.id"
        :class="'task_item_lab task_item_lab_' + isCheckedOn"
      ></label>
    </span>
  </div>
</template>
<style lang="scss" scoped>
@import "@/assets/styles/todo";
.task_item {
  padding: 0.5em 0 0.5em 0.5em;
  font-size: 0.8rem;
  display: grid;
  grid-template-columns: 4em 1fr 4em;
  position: relative;

  .task_id {
    text-align: right;
    padding-right: 1em;
    .delete_task {
      color: $cultured;
      text-align: center;
      border-radius: 0 1em 1em 0;
      padding-top: 0.5em;
      content: "x";
      position: absolute;
      width: 1.75em;
      height: 100%;
      background-color: darken($rusty-red, 25%);
      top: 0;
      left: 0;
      &:hover {
        background-color: $rusty-red;
      }
    }
  }

  .task_status {
    position: relative;
    margin-right: 1em;
    .task_item_lab {
      position: absolute;
      width: 100%;
      height: 100%;
      border-radius: 1em;
      display: flex;
      align-items: center;
      &:before {
        content: "";
        position: absolute;
        width: 1em;
        height: 1em;
        background-color: darken($green-pantone, 25%);
        box-shadow: 2px 2px 5px -2px $gunmetal;
        border-radius: 0.5em;
        margin-left: 0.15em;
      }
    }
    .task_item_check {
      display: none;
    }

    .task_item_lab_off {
      background-color: lighten($rusty-red, 25%);
      box-shadow: -1px -1px 5px -3px $gunmetal inset;
      &:before {
        background-color: darken($rusty-red, 25%);
        box-shadow: 2px 2px 5px -2px $gunmetal;
        transform: translate(165%);
      }
    }

    .task_item_lab_on {
      background-color: lighten($green-pantone, 25%);
      box-shadow: -1px -1px 5px -3px $gunmetal inset;
    }
  }
}

.task_item_off {
  color: darken($cultured, 50%);
  text-decoration-line: line-through;
}
</style>
<script>
export default {
  name: "Task",
  created: function () {
    this.checked = this.task_item.status === "active";
  },
  props: { task_item: null },
  data: function () {
    return { checked: Boolean };
  },
  computed: {
    isCheckedOn: function () {
      return this.checked ? "on" : "off";
    },
  },
  methods: {
    fnEmitTaskChanged: function () {
      this.$emit("fnEmitTaskChanged", {
        task_id: this.task_item.id,
        task_status: this.checked,
      });
    },

    fnEmitDeleteTask: function () {
      this.$emit("fnEmitDeleteTask", { task_id: this.task_item.id });
    },
  },
};
</script>
