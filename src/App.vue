<template>
  <div id="app">
    <header>
      <div class="header">
        <ToDoForm @newTodo="newTodo"/>
      </div>
    </header>
    <main>
      <ToDoList :todoList="todoList" @changeCurrentFilter="changeFilter"/>
    </main>
  </div>
</template>

<script>
import ToDoForm from "./components/ToDoForm.vue"
import ToDoList from "./components/ToDoList.vue"

export default {
  name: 'App',
  components: { ToDoForm, ToDoList },
  data() {
    return {
      todoList: [
        {
          title: "Hello World",
          checked: false,
          done: false
        }
      ],
      filterList: [],
      currentFilter: "All"
    }
  },
  methods: {
    newTodo(value){
      let todo = {
        title: value,
        checked: false,
        done: false,
      }
      this.todoList.push(todo);
    },
    changeFilter(value){
      this.currentFilter = value;
    },
    UpdateFilterList() {
      if (this.currentFilter === "All") {
        this.filterList = this.todoList;
      } else if (this.currentFilter === "Active") {
        this.todoList.forEach(element => {
          if(!element.done) {
            this.filterList.push(element);
          }
        });
      } else {
        this.todoList.forEach(element => {
          if(element.done) {
            this.filterList.push(element);
          }
        })
      }
    }
  },
  computed: {
    todoListUpdated: function(){
      this.UpdateFilterList();
      return this.filterList;
    },
  }
}
</script>

<style lang="sass">
body
  margin: 0
  padding: 0
  box-sizing: border-box
  font-family: 'Josefin Sans', sans-serif
  background-color: hsl(0, 0%, 98%)

.header
  background-image: url("./assets/bg-desktop-light.jpg")
  background-repeat: no-repeat
  height: 50vh
  width: 100%
  background-color: linear-gradient(to right, hsl(192, 100%, 67%), hsl(280, 87%, 65%))
  margin: 0

main
  display: flex
  flex-direction: column
  justify-content: center
  align-items: center
  height: 100%
  margin: 0
</style>
