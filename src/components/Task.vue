<template>
  <div class="task" v-bind:id="taskId">
    <h3>{{taskName}}</h3>
    <button class="disposeBtn" v-on:click="disposeTask()">X</button>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    taskId: Number,
    taskName: String
  },
  methods: {
    disposeTask: function() {
      this.$emit("delete-task", this.taskId);
      this.$destroy();
      document.getElementById(this.taskId).remove();
    }
  }
};
</script>

<style>
.task {
  /*box-sizing: border-box;*/
  width: 90%;
  padding: 0 1%;
  border: 2px solid green;
  border-radius: 15px;
  height: auto;
  margin: 1% 0;
}

.task > * {
  display: inline-block;
}

.disposeBtn {
  color: white;
  background-color: firebrick;
  border-radius: 10px;
}

.disposeBtn:hover {
  color: firebrick;
  background-color: white;
  font-weight: bold;
}
</style>