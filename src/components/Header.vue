<template>
  <header>
    <h1>{{ title }}</h1>
    <AddTaskButton
    v-show="homePage"
    @btn-click="$emit('toggle-add-task')"
    :buttonText="showAddTask ? 'Close Form -' : 'Add Task +'"
    :buttonColor="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
  import AddTaskButton from "./AddTaskButton";

  export default {
    name: "Header",
    props: {
      title: {
        default: "Please Add A Title",
        type: String,
        required: true
      },
      showAddTask: {
        type: Boolean
      }
    },
    components: {
      AddTaskButton,
    },
    computed: {
      homePage() {
        if (this.$route.path === '/') {
          return true;
        } else {
          return false;
        }
      }
    },
    emits: ['toggle-add-task']
  }
</script>

<style scoped>
  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 0 0 20px 0;
  }
</style>