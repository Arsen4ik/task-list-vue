<template>
  <section>
    <div v-for="taskDay in Object.entries(tasks)" :key="taskDay[0]">
      <!-- <div v-if="taskDay[1].length">
        {{ taskDay[0] }}
      </div> -->
      <task-item
        v-if="taskDay[1].length"
        :dayTaskList="taskDay"
        @deleteTask="deleteTask"
        @deleteDay="deleteDay"
      ></task-item>
    </div>
  </section>
</template>
<script>
import TaskItem from './TaskItem.vue'

export default {
  props: ['tasks'],
  emits: ['deleteTask', 'deleteDay'],
  methods: {
    deleteTask(day, id) {
      this.$emit('deleteTask', day, id)
    },
    deleteDay(day) {
      this.$emit('deleteDay', day)
    }
  },
  components: {
    TaskItem
  }
}
</script>
<style scoped>
section {
  width: 1088px;
  margin-top: 25px;
  display: flex;
  flex-direction: column;
}
</style>
