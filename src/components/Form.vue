<template>
  <form @submit.prevent="addNewTask">
    <div class="inputs">
      <select required v-model="weekDay">
        <option value="ПН">ПН</option>
        <option value="ВТ" selected>ВТ</option>
        <option value="СР">СР</option>
        <option value="ЧТ">ЧТ</option>
        <option value="ПТ">ПТ</option>
        <option value="СБ">СБ</option>
        <option value="ВС">ВС</option>
      </select>
      <select required v-model="isImportant">
        <option value="important">важно</option>
        <option value="" selected>не важно</option>
      </select>
      <input v-model="description" required type="text" placeholder="описание" />
    </div>
    <button>Добавить</button>
  </form>
</template>
<script>
export default {
  emits: ['addTask'],
  data() {
    return {
      weekDay: '',
      isImportant: '',
      description: ''
    }
  },
  methods: {
    addNewTask() {
      //   console.log(this.weekDay, this.isImportant, this.description)
      this.$emit('addTask', {
        weekDay: this.weekDay,
        isImportant: this.isImportant,
        description: this.description
      })
    }
  }
}
</script>
<style scoped>
form {
  width: 1088px;
  background-color: #ecf0f1;
  display: flex;
  flex-direction: row;
  padding: 30px 55px;
  margin-top: 80px;
  border-radius: 20px;
  border: 1px solid black;
  box-shadow:
    0 20px 25px -5px rgb(0 0 0 / 0.1),
    0 8px 10px -6px rgb(0 0 0 / 0.1);

  div {
    width: 60%;
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    grid-template-rows: repeat(2, 1fr);
    column-gap: 35px;
    row-gap: 25px;

    input,
    select {
      height: 45px;
      padding: 0 10px;
      border: 1px solid black;
    }

    input {
      grid-column-start: 1;
      grid-column-end: 3;
    }
  }

  button {
    width: 163px;
    height: 45px;
    border-radius: 50px;
    background-color: #1abc9c;
    color: white;
    border: 1px solid black;
    font-size: 20px;
    align-self: end;
    position: relative;
    left: 230px;
  }
}
</style>
