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
  box-sizing: border-box;
  width: 400px;
  padding: 0 1%;
  position: relative;
  border: 2px solid green;
  border-radius: 15px;
  height: 66px;
  margin: 2% 0;
}

.task > * {
  display: inline-block;
}

.task:only-child {
  width: 100%;
  height: auto;
}

.disposeBtn {
  color: white;
  background-color: firebrick;
  border-radius: 10px;
  position: absolute;
  top: 19px;
  right: 15px;
}

.disposeBtn:hover {
  color: firebrick;
  background-color: white;
  font-weight: bold;
}
</style>