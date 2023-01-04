<template>
  <div class="container">
    <!-- 3. and then using component here -->
    <Header @toggle-add-task="toggleAddTask" title="Task Tracker" v-bind:showAddTask="showAddTask" />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
    <Tasks @toggle-reminder="toggleReminder" @delete-task="deleteTask" v-bind:tasks="tasks" />
  </div>
</template>

<!-- 0. creating a Header component in /components -->

<script>
// 1. Importing component
import Header from './components/Header'
import Tasks from './components/Tasks'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    // 2. Registering the imported component
    Header,
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id ?
        { ...task, reminder: !task.reminder } : task)
    },
    addTask(task) {
      // this.tasks.push(newTask) detta m arg=newTask funkar också
      this.tasks = [...this.tasks, task]
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = res.json();
      return data;
    },
    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = res.json();
      return data;
    }
  },
  async created() {
    this.tasks = await this.fetchTasks()
  },
  //   created() {
  //     this.tasks = [
  //       {
  //         id: 1,
  //         text: 'Öva på VUE',
  //         day: 'Varje dag innan/efter lunch',
  //         reminder: true,
  //       },
  //       {
  //         id: 2,
  //         text: 'Öva på react',
  //         day: 'Varje kväll innan/efter middag',
  //         reminder: true,
  //       },
  //       {
  //         id: 3,
  //         text: 'Skriv om CV',
  //         day: 'Någon dag innan jan slut',
  //         reminder: false,
  //       },
  //     ]
  //   }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
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
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}

.btn:focus {
  outline: none;
}

.btn:active {
  transform: scale(0.98);
}

.btn-block {
  display: block;
  width: 100%;
}
</style>
