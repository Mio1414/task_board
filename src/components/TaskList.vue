<template>
  <h1>{{ title }}</h1>
  <h2>{{ titelTask }}</h2>
  <button @click="addTask">Добавить задание</button>
  {{ list }}
  <div class="task-list">
    <ul>
      <li 
      v-for="task in list" 
      v-bind:key='task'
      >
        Задание 1 {{ task.title}}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'task-list',
  data() {
    return{
      titleTask: 'Заголовок компонента',
      list:[
        {
          title:'Помыть посуду'
        },
        {
          title:'Постирать'
        }
      ]
    };
  },
  props: {
    title: String
  },
  methods:{

    hello(){
      alert('Привет');
      // Нельзя заменять заголовок из props
      
      this.titleTask = 'Заголовок'
    },
    addTask(){
      const newTask = prompt ('Введите название задачи');
      this.list.push({
        title: newTask
      })
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
