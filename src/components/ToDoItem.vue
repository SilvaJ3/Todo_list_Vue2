<template>
  <div class="todo" :class="darkMode ? 'darkModeItem' : ''" @mouseover="DisplayDeleteBtn()">
    <div class="todo_main">
      <div class="left_part">
        <div class="checkBox" :class="this.data.done ? 'done' : ''" @click="CheckTodo()">
          <img src="../assets/icon-check.svg" alt="" :v-show="this.data.done">
        </div>
      </div>
      <h1 :class="this.data.done ? 'done' : ''" >{{data.title}}</h1>
      <div class="cross" @click="DeleteTodo()">
        <img src="../assets/icon-cross.svg" alt="" v-if="this.displayDeleteBtn">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return {
      displayDeleteBtn: false
    }
  },
  props: {
    data: Object,
    darkMode: Boolean
    },
  methods: {
    CheckTodo() {
      this.data.done = !this.data.done;
      this.$emit("TodoDone", this.data);
    },
    DisplayDeleteBtn(){
      this.displayDeleteBtn = !this.displayDeleteBtn;
    },
    DeleteTodo(){
      this.$emit("DeleteTodo", this.data);
    }
  }
}
</script>

<style lang="sass">
.todo
  width: 100%
  margin: 0
  background-color: white
  border-bottom: solid 1px lightgrey
  .todo_main    
    display: flex
    align-items: center
    width: 100%
    .left_part
      width: 60px
    .checkBox
      border-radius: 50%
      width: 20px
      height: 20px
      cursor: pointer
      border: solid 1px grey
      margin: auto 30px auto 20px
      display: flex
      justify-content: center
      align-items: center
    .done
      background: linear-gradient(135deg, rgb(87, 221, 255), rgb(192, 88, 243)) !important
      width: 25px
      height: 25px
      border: none
      img
        pointer-events: none
        width: 12px
        height: 12px
    .done
      text-decoration: line-through
    h1
      overflow-x: scroll
      width: 80%
    h1::-webkit-scrollbar
      display: none
    .cross
      cursor: pointer
.darkModeItem
  background-color: hsl(235, 24%, 19%) !important
  color: white

</style>