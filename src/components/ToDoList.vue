<template>
  <section>
    <div class="todoList">
      <ToDoItem v-for="(todo, index) in todoList" :key="index" :data="todo" @TodoDone="TodoDone"/>
      <div class="summary">
        <div class="items_count">
          <span>
            {{ todoList.length}} items left
          </span>
          </div>
        <div class="categories">
          <span :class="currentFilter === 'All' ? 'active' : ''" @click="changeFilter('All')">All</span>
          <span :class="currentFilter === 'Active' ? 'active' : ''" @click="changeFilter('Active')">Active</span>
          <span :class="currentFilter === 'Completed' ? 'active' : ''" @click="changeFilter('Completed')">Completed</span>
        </div>
        <div class="clear" @click="clearCompleted()">
          <span>Clear Completed</span>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import ToDoItem from "./ToDoItem.vue"

export default {
  data() {
    return {
      currentFilter: "All",
    }
  },
  components: {
    ToDoItem
  },
  props: {
    todoList: Array
  },
  methods: {
    changeFilter: function(filter){
      this.currentFilter = filter;
      this.$emit("changeCurrentFilter", filter);
    },
    clearCompleted: function() {
      this.$emit("clearCompleted");
    },
    TodoDone: function(value){
      this.$emit("TodoDone", value);
    }
  }
}
</script>

<style lang="sass">
.todoList
  margin-top: -20%
  width: 37vw
  display: flex
  flex-direction: column
  box-shadow: 0px 0px 5px rgba(0, 0, 0, 0.5)
  border-radius: 5px
  overflow: hidden
  .summary
    display: flex
    justify-content: center
    align-items: center
    background-color: white
    color: grey
    padding: 15px 0
    .items_count
      font-size: 14px
    .categories
      margin: auto 15%
      span:nth-child(2)
        margin: auto 5%
      span
        cursor: pointer
        font-weight: 700
      .active
        color: hsl(235, 19%, 35%) !important
      span:hover
        color: hsl(235, 19%, 35%)
    .clear
      font-size: 14px
      span
        cursor: pointer
      span:hover
        color: hsl(235, 19%, 35%) !important
</style>