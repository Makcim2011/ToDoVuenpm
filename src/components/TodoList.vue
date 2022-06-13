<template>
  <div class="hello">
    <div>{{ title }}</div>
    <label>Додати нове завдання <input v-model="newTask"/></label>
    <button v-on:click="addTask()">Add Task</button>
    <p v-if="tasks.length">
    <ul v-for="(task, key) in tasks" :key="`task-${key}`">
    <li>{{task.text}}</li>
    </ul>
    </p>
    <p v-else>Tere are no tasks yet</p>
  </div>
</template>

<script>
export default {
  name: 'TodoList',
  data() {
    return {
      title: 'My ToDoList',
      newTask: '',
      tasks: [],
    }
  },
  methods: {
    addTask: function() {
      this.tasks.push({text: this.newTask, completed: false})
      this.newTask = ''
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
