<template>
  <div id="app">
    <task-list ></task-list>
  </div>
</template>

<script>


import TaskList from "./components/TaskList";

export default {
  data() {
    return{

    }
  },
  components: {
    TaskList,
  }
}
</script>

<style lang="scss" scoped>

</style>
