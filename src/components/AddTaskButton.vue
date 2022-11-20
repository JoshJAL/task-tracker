<template>
  <button @click="onClick()" :style="{ background: buttonColor }" class="btn" >
    {{ buttonText }}
  </button>
</template>

<script>
  export default {
    name: "AddTaskButton",
    props: {
      buttonText: {
        type: String,
        default: "Add Button Text",
        required: true
      },
      buttonColor: {
        type: String,
        default: "black",
      }
    },
    methods: {
      onClick() {
        this.$emit('btn-click');
      }
    }
  }
</script>