<template>
    <AddTask v-if="showAddTask" @add-task="addTask" />
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
    <p v-show="tasksAvailable">(Double Click Task to Toggle Reminder)</p>
</template>

<script>
  import AddTask from "../components/AddTask";
  import Tasks from "../components/Tasks";

  export default {
    name: "Home",
    props: {
      showAddTask: {
        type: Boolean
      }
    },
    components: {
      AddTask,
      Tasks,
    },
    data() {
      return {
        tasks: [],
      }
    },
    methods: {
    async addTask(task) {
      const res = await fetch('api/tasks', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(task)
      });

      const data = await res.json();

      this.tasks = [...this.tasks, data];
    },
    async deleteTask(id) {
      if (confirm("Are you sure you want to delete this Task?\n\nThis cannot be undone.")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: 'DELETE',
        });

        res.status == 200 ? (this.tasks = this.tasks.filter((task) => task.id !== id)) : alert("Error Deleting Task");
      }
    },
    async toggleReminder(id) {
      const taskToToggle = await this.fetchTask(id);
      const updatedTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updatedTask),
      });

      const data = await res.json();

      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: data.reminder} : task);
    },
    async fetchTasks() {
      const res = await fetch('api/tasks');
      const data = await res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  computed: {
    tasksAvailable() {
      if (this.tasks.length > 0) {
        return true;
      } else {
        return false;
      }
    }
  }
  }
</script>

<style scoped>
 p {
  text-align: center;
 }
</style>