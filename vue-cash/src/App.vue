<template>
  <div class="container">
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" :showAddTask="showAddTask"
     />

    <div v-show="showAddTask">
      <AddTask @add-task="addTask"  />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" :tasks="tasks"/>
  </div>
  <router-view/>
</template>
<script>
  import  Header  from './components/Header'
  import  Tasks  from './components/Tasks'
  import  AddTask  from './components/AddTask'


  export default {
    name: 'App',
    components: {
    Header,
    Tasks,
    AddTask

},
    data() {
      return {
        tasks: [],
        showAddTask: false
      }
    },
    methods :{
      toggleAddTask(){
        this.showAddTask = !this.showAddTask
      },
      addTask(task){
        this.tasks =[...this.tasks,task]
      },

      deleteTask(id){
        if(confirm ('Are you delete ?')){
          this.tasks= this.tasks.filter((task) =>task.id !==id)
        }
      },
      toggleReminder(id){
        this.tasks =this.tasks.map((task)=> task.id === id ?
        {...task, reminder: !task.reminder}:task)
      },
    },
    created(){
      this.tasks = [
        {
          id :1,
          text:  'Doctors Apponmtment',
          day : 'March 1st at 2:30pm',
          reminder: true,
        },
        {
          id :2,
          text:  'Meeting office',
          day : 'March 3rd at 1:30pm',
          reminder: true,
        },
        {
          id :3,
          text:  'Go to school',
          day : 'March 3rd at 11:30pm',
          reminder: true,
        },
      ]
    }
  }

</script>
<style>
 @import url('https://fonts.googleapis.com/css2?family=Popins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins',sans-serif;
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
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px ;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size:15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn:block {
  display: block;
  width: 100%;
}



/* #app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
} */
</style>
