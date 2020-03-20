<template>
  <div id="taskList">
    <Task
      v-for="task in tasks"
      :key="task.taskId"
      :taskName="task.taskName"
      :taskId="task.taskId"
      @delete-task="sendDeleteRequest"
    />
  </div>
</template>

<script>
import Task from "@/components/Task.vue";

export default {
  name: "TaskList",
  components: {
    Task
  },
  props: {
    tasks: Array
  },
  methods: {
    sendDeleteRequest: function(idx) {
      this.$emit('delete', idx);
    }
  }
};
</script>

<style>
</style>