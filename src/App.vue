<template>
  <div class="container">
    <Header @toggle-add-task="addToggleTask" title="Track" :showAddTask="showAddTask" />
    <div v-if="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks" />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  methods: {
    addToggleTask(){
      this.showAddTask = !this.showAddTask
    },
    addTask(task){
        this.tasks = [...this.tasks, task]
    },
    deleteTask(id) {
      if(confirm("delete file?")){
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id){
      this.tasks = this.tasks.map((task)=> task.id === id ? {...task, reminder: !task.reminder}: task)
    }
  },
  data() {
    return {
      tasks: [],
      showAddTask: false
    };
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: "Abduraxim was born",
        day: "19th december 1999",
        reminder: true,
      },
      {
        id: 2,
        text: "Barceelona was created",
        day: "january 1st march 1999",
        reminder: true,
      },
      {
        id: 3,
        text: "Chelsea was created",
        day: "march 1st march 2009",
        reminder: true,
      },
    ];
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,600;0,700;1,400;1,500&display=swap');
*{
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
body{
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background-color: black;
  color: white;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
}
</style>