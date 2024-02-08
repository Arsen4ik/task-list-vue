<template>
  <Form @addTask="addTask"></Form>
  <task-list :tasks="tasks" @deleteTask="deleteTask" @deleteDay="deleteDay"></task-list>
</template>
<script>
import Form from './components/Form.vue'
import TaskList from './components/TaskList.vue'

export default {
  components: {
    Form,
    TaskList
  },
  data() {
    return {
      // tasks: [
      //   // {
      //   //   id: 1,
      //   //   weekDay: 'пн',
      //   //   tasks: [
      //   //     {
      //   //       id: 1,
      //   //       task: '',
      //   //       isImportant: false,
      //   //     }
      //   //   ]
      //   // }
      // ]
      // tasks: {
      //   'пн': [

      //   ]
      // }
      tasks: {
        ПН: [],
        ВТ: [],
        СР: [],
        ЧТ: [],
        ПТ: [],
        СБ: [],
        ВС: []
      }
    }
  },
  methods: {
    addTask(task) {
      // console.log(task)
      this.tasks[task.weekDay].push({
        id: new Date().getTime(),
        isImportant: task.isImportant,
        description: task.description
      })
    },
    deleteTask(day, id) {
      // console.log(day, id)
      this.tasks[day].splice(
        this.tasks[day].findIndex((task) => task.id === id),
        1
      )
    },
    deleteDay(day) {
      this.tasks[day].length = 0
    }
  }
}
</script>
<style scoped></style>
