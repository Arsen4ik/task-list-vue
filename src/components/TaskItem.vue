<template>
  <!-- <div>{{ dayTaskList }}</div> -->
  <div class="dayTasks" @click="deleteDay(dayTaskList[0])">
    <p class="day">{{ dayTaskList[0] }}</p>
    <div>
      <p
        v-for="task in dayTaskList[1].sort(
          (taskA, taskB) => (taskB.isImportant ? 1 : 0) - (taskA.isImportant ? 1 : 0)
        )"
        :key="task.id"
        :class="task.isImportant ? 'red' : 'green'"
        @click="deleteTask($event, dayTaskList[0], task.id)"
        @mouseenter="hideAfter"
        @mouseleave="showAfter"
      >
        {{ task.description }}
      </p>
    </div>
  </div>
  <!-- {{ dayTaskList[1].sort((taskA, taskB) => taskA.isImportant - taskB.isImportant) }} -->
</template>
<script>
export default {
  props: ['dayTaskList'],
  emits: ['deleteTask', 'deleteDay'],
  // data() {
  //   return {
  //     dayTasks: this.dayTaskList.sort((taskA, taskB) => taskA.isImportant - taskB.isImportant)
  //   }
  // },
  methods: {
    deleteTask(e, day, id) {
      //   e.preventDefault()
      e.stopPropagation()

      this.$emit('deleteTask', day, id)
    },
    deleteDay(day) {
      //   e.preventDefault()
      //   e.stopPropagation()

      this.$emit('deleteDay', day)
    },
    hideAfter(event) {
      event.currentTarget.parentNode.parentNode.classList.add('hide-after')
      //   console.log(event.currentTarget.parentNode.classList)
      //   console.log(event.currentTarget.parentNode)
    },
    showAfter(event) {
      event.currentTarget.parentNode.parentNode.classList.remove('hide-after')
      //   console.log(event.currentTarget.parentNode.classList)
      //   console.log(event.currentTarget.parentNode)
    }
  }
}
</script>
<style scoped>
.red {
  background-color: #e74c3c;
}
.green {
  background-color: #1abc9c;
}

.dayTasks {
  margin-top: 30px;
  position: relative;
  display: flex;
  flex-direction: row;
  border-radius: 20px;
  box-shadow:
    0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  &::after {
    content: '✖️';
    /* content: url(../assets/close.svg);
        height: 15px;
        width: 15px;
        background-size: 20px; */
    border: 1px solid rgb(26, 26, 26);
    border-radius: 100%;
    padding: 1px 3px;
    background-color: #e74c3c;
    font-size: medium;
    display: none;
    position: absolute;
    top: -10px;
    right: -8px;
  }

  &:hover {
    &::after {
      display: inline;
    }
  }

  .day {
    font-size: 30px;
    font-weight: 400;
    background-color: #34495e;
    border-radius: 20px 0 0 20px;
    padding: 10px;
    color: white;
    display: flex;
    align-items: center;
  }

  div {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    width: 100%;
    height: min-content;
    background-color: white;
    border-radius: 0 20px 20px 0;
    padding: 15px 30px;

    p {
      font-size: 30px;
      padding: 10px 20px;
      color: white;
      position: relative;

      &::after {
        content: '✖️';
        /* content: url(../assets/close.svg);
        height: 15px;
        width: 15px;
        background-size: 20px; */
        border: 1px solid rgb(26, 26, 26);
        border-radius: 100%;
        padding: 1px 3px;
        background-color: #e74c3c;
        font-size: medium;
        display: none;
        position: absolute;
        top: -10px;
        right: -8px;
      }

      &:hover {
        &::after {
          display: inline;
        }
      }
    }
  }
}

.hide-after::after {
  display: none !important;
}
</style>
