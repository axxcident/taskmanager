<template>
  <div class="container">
    <!-- 3. and then using component here -->
    <Header title="Task Tracker" />
    <Tasks @delete-task="deleteTask" v-bind:tasks="tasks" />
  </div>
</template>

<!-- 0. creating a Header component in /components -->

<script>
// 1. Importing component
import Header from './components/Header'
import Tasks from './components/Tasks'

export default {
  name: 'App',
  components: {
    // 2. Registering the imported component
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id) {
      console.log('task', id)
    }
  },
  created() {
    this.tasks = [
      {
        id: 1,
        text: 'Öva på VUE',
        day: 'Varje dag innan/efter lunch',
        reminder: true,
      },
      {
        id: 2,
        text: 'Öva på react',
        day: 'Varje kväll innan/efter middag',
        reminder: true,
      },
      {
        id: 3,
        text: 'Skriv om CV',
        day: 'Någon dag innan jan slut',
        reminder: false,
      },
    ]
  }
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
