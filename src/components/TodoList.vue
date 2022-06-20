<template>
  <div class="main">
    <div>{{ title }}</div>
    <div>{{ tasks }}</div>
    <label>Додати нове завдання<input v-on:keyup.enter="addTask()" v-model="newTask"/></label>
    <button v-on:click="addTask()">Add Task</button>
    <p v-if="tasks.length">
    <ul v-for="task in sortedtasks" :key="task.key">
      <li class="liTask">
        <input type="checkbox" v-model="task.completed">
        <p class="liTaskText"
        :class="{liTaskText_isShow: task.completed}"
        >{{task.text}}</p>
        <button class="deleteBtn" v-on:click="removeTask(task.key)" role="button">&#10006;     |  {{task.key}}</button>
      </li>
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
  mounted() {
        if (localStorage.getItem('tasks')) {
      try {
        this.tasks = JSON.parse(localStorage.getItem('tasks'));
      } catch(e) {
        localStorage.removeItem('tasks');
      }
    }
  },
  watch: {
    tasks: {
      handler() {
          const parsed = JSON.stringify(this.tasks)
          localStorage.setItem('tasks', parsed)
      },
      deep: true
    }
  },
  methods: {
    addTask() {
      if(this.newTask !== '') {
      this.tasks.push({text: this.newTask, completed: false, key: Math.floor((Math.random() * 10e12) + 1)})
      this.newTask = ''
      }
    },
    removeTask(key) {
      let indextask = obj => obj.key === key;
      this.tasks.splice((this.tasks.findIndex(indextask)), 1)
    }
  },
  computed: {

  sortedtasks() {
      return [].concat(this.tasks).sort(function(a, b) {
        if (a.completed > b.completed) {
          return 1;
        }
        if (a.completed < b.completed) {
          return -1;
        }
        return 0;
      })
    }
  }
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
.main {
  background-color: aquamarine;
  min-height: 300px;
  max-width: 500px;
  margin: 10px;
  width: 100%;
  padding: 10px;
  ul {
  padding: auto;
  }
  .liTask{
    border-radius: 15px;
    background-color: aqua;
    max-width: 400px;
    list-style-type: none;
    text-align: start;
    margin-block-start: auto;
    padding: 2px;
    margin: 5px;
    display: flex;
    align-content: flex-start;
    justify-content:start;
    align-items: baseline;
    .liTaskText{
      padding-left: 1px;
      max-width: fit-content;
      margin: 0.5rem;
      flex-shrink: 1;
      flex-grow: 1;
      text-align: start;
      margin-left: 5px;

      &_isShow {
        text-decoration-line:line-through
      }
    }
    .deleteBtn {
      background-color: transparent;
      border: none;
      margin-right: 2px;
      margin-left: auto;
    }
  }

}
</style>
