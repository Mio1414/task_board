<template>
  <h1>{{ title }}</h1>
  {{ list }}
  <div class="task-list">
    <ul>
      <li @click="hello">Задание 1</li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'task-list',
  data() {
    return{
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
    }

  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
