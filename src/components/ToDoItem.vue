<template>
  <div class="todo">
    <div class="todo_main">
      <div class="left_part">
        <div class="checkBox" :class="this.data.checked ? 'checked' : ''" @click="CheckTodo()">
          <img src="../assets/icon-check.svg" alt="" :v-if="this.data.checked">
        </div>
      </div>
      <h1 :class="this.data.checked ? 'done' : ''">{{data.title}}</h1>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    data: Object
  },
  methods: {
    CheckTodo() {
      this.data.checked = !this.data.checked;
      this.$emit("TodoDone", this.data);
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
    .checked
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
    h1::-webkit-scrollbar
      display: none

</style>