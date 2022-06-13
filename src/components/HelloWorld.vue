<template>
  <div class="hello">
    <!-- <div>{{ title }}</div> -->
    <label>Додати нове завдання <input v - model = "newTask" /></label>
    <ul v - for = "index in tasks">
      <li>{{ index.text }}</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      // title: 'ToDoList',
      newTask: '',
      tasks: [
        {
          text: 'Завдання для виконання 1',
          completed: false,
        },
        {
          text: 'Завдання для виконання 2',
          completed: false,
        },
        {
          text: 'Завдання для виконання 3',
          completed: false,
        }
      ]
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
