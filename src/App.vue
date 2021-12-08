<template>
  <div id="app">
    <header :class="darkMode ? 'darkMode' : ''">
      <div class="header" :class="darkMode ? `dark` : `light`">
        <ToDoForm @newTodo="newTodo" :darkMode="darkMode" @switchMode="switchMode"/>
      </div>
    </header>
    <main :class="darkMode ? 'darkMode' : ''">
      <ToDoList 
      :todoList="todoListUpdated" 
      :darkMode="darkMode"
      @changeCurrentFilter="changeFilter" 
      @TodoDone="TodoDone"
      @clearCompleted="clearCompleted"
      @DeleteTodo="DeleteTodo"
      />
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
        // {
        //   title: "Hello World",
        //   done: false
        // }
      ],
      filterList: [],
      currentFilter: "All",
      darkMode: true,
      BgLightMode: "./assets/bg-desktop-light.jpg",
      BgDarkMode: "./assets/bg-desktop-dark.jpg",
    }
  },
  methods: {
    // Ajout d'une tâche
    newTodo(value){
      let todo = {
        title: value,
        done: false,
      }
      this.todoList.push(todo);
    },
    // Modification du filtre
    changeFilter(value){
      this.currentFilter = value;
    },
    // Tâche complétée
    TodoDone(value){
      let index = this.todoList.indexOf(value);
      this.todoList[index].done = !this.todoList[index].done;
    },
    // Suppression d'une tâche
    DeleteTodo(value){
      let index = this.todoList.indexOf(value);
      this.todoList.splice(index, 1);
    },
    // Suppression des tâches complétées
    clearCompleted(){
      for (let index = 0; index < this.todoList.length; index++) {
        let element = this.todoList[index];
        if(element.done) {
          this.todoList.splice(index, 1);
          index--;
        }
      }
    },
    // Mise à jour de la liste des tâches
    UpdateFilterList() {
      if (this.currentFilter === "All") {
        this.filterList = this.todoList;
      } else if (this.currentFilter === "Active") {
        this.filterList = [];
        this.todoList.forEach(element => {
          if(!element.done) {
            this.filterList.push(element);
          }
        });
      } else {
        this.filterList = [];
        this.todoList.forEach(element => {
          if(element.done) {
            this.filterList.push(element);
          }
        })
      }
    },
    // Changement de thème
    switchMode(){
      this.darkMode = !this.darkMode;
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

// #app

.header
  height: 50vh
  width: 100%
  margin: 0
.light
  background-image: url("./assets/bg-desktop-light.jpg")
  background-repeat: no-repeat
  background-color: hsl(0, 0%, 98%)

.dark
  background-image: url("./assets/bg-desktop-dark.jpg")
  background-repeat: no-repeat

main
  background-color: hsl(0, 0%, 98%)
  display: flex
  flex-direction: column
  justify-content: start
  align-items: center
  min-height: 50vh
  margin: 0
.darkMode
  background-color: hsl(235, 24%, 19%) !important
</style>
