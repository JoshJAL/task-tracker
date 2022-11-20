<template>
  <div @dblclick="$emit('toggle-reminder', task.id)" :class="[task.reminder ? 'reminder' : '', 'task']">
    <h3>
      {{ task.text }}
      <i @click="$emit('delete-task', task.id)" class="fas fa-times"></i>
    </h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<script>
  export default {
    name: "Task",
    props: {
      task: {
        type: Object,
        required: true,
      }
    },
  }
</script>

<style scoped>
  .fas {
    color: red;
    cursor: pointer;
  }

  .task {
    background: #f4f4f4;
    padding: 10px 20px;
    margin: 5px;
    cursor: pointer;
  }

  .task.reminder {
    border-left: 5px solid green;
  }

  .task h3 {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

</style>