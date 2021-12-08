<template>
  <section>
    <div class="todoForm">
      <div class="heading">
        <h1>TODO</h1>
        <img :src="darkMode ? moon : sun" alt="" @click="() => this.$emit('switchMode')">
      </div>
      <div class="form">
        <form @submit.prevent :class="darkMode ? 'darkMode' : ''">
          <div class="checkBox">
          </div>
          <input type="text" placeholder="Create a new todo..." v-model="todo" @keydown.enter="Submit">
        </form>
      </div>
    </div>
  </section>
</template>

<script>
import moon from "../assets/icon-moon.svg";
import sun from "../assets/icon-sun.svg";

export default {
  data(){
    return {
      todo: "",
      moon: moon,
      sun: sun
    }
  },
  methods: {
    Submit() {
      if (this.todo) {
        this.$emit("newTodo", this.todo);
        this.todo = "";
      }
    }
  },
  props: {
    darkMode: Boolean
  }
}
</script>

<style lang="sass">
.todoForm
  display: flex
  flex-direction: column
  margin: auto
  width: 37vw
  .heading
    display: flex
    justify-content: space-between
    align-items: center
    color: white
    h1
      letter-spacing: 15px
      font-size: 45px
    img
      cursor: pointer
  .form
    width: 100%
    padding: auto 5%
  form
    background-color: white
    height: 70px
    border-radius: 5px
    display: flex
    align-items: center
    width: 100%
    .checkBox
      border-radius: 50%
      width: 35px
      height: 20px
      cursor: pointer
      border: solid 1px grey
      margin: auto 2% auto 4%
    input
      border: none
      font-family: 'Josefin Sans', sans-serif
      font-size: 20px
      padding-left: 3%
      height: 40px
      border-radius: 15px
      width: 150%
    input:focus
      outline: none
  .darkMode
    background-color: hsl(235, 24%, 19%) !important
    input
      background-color: hsl(235, 24%, 19%) !important
      color: white
</style>