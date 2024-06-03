<template>

  <div class="conteiner" :style="{ backgroundImage: `url(${srcList[currentPageBg].src})`}">
    <button @click="toggleMenu">Сменить фон</button>
    <div :class="visibleMenu ? 'menu active' : 'menu'">
      <button 
        v-for="(img, index) in srcList" 
        :key="img.id" 
        class="img-button-conteiner"
        
        >
        <img :src="img.src" 
        class="img-button" 
        :data-index="index"
        @click="cangeBg"
        >
      </button>
    </div>

   
    <button @click="switchModel">Добавить задание</button>
  
    <div class="task-list">
      <ul>
        <li 
        v-for="(task,index) in list" 
        v-bind:key='task'
        >
          Задание {{index + 1}} {{ task.title}}
          <button @click="dellTask(index)">Удалить</button>
          <!-- Сделать функцию, которую мы будем открывать в попапе текст и в нем редактировать -->
          <button>Редактировать</button>
        </li>
      </ul>
 
    </div>

    <div class="overlay" v-if="isShowModel">
      <div>

        <form>
          <button class="close" @click="switchModel">Закрыть</button>
          <div class="form-content">
            <div>Добавить задание:</div>
            <div><input type="text" v-model="textNewTask"></div>
            <button @click="addTask">Добавить</button>
          </div>
        </form>
      </div>
    </div>



  </div>
</template>
  

<script>
export default {
  name: 'task-list',
  data() {
    return{
      textNewTask:'',
      isShowModel: false,
      currentPageBg:0,

      visibleMenu: false,

      srcList: [
        {
          id:'fddfjknfdj',
          src:'https://klevtsovaelena.github.io/wallpaper/img/BlackWhite6.jpg'
        },
        {
          id:'fdvffvf',
          src:'https://klevtsovaelena.github.io/wallpaper/img/BlackWhite5.jpg'
        },
        {
          id:'gbffhgnfdh',
          src:'https://klevtsovaelena.github.io/wallpaper/img/BlackWhite9.jpg'
        },
        {
          id:'fdvbdghvf',
          src:'https://klevtsovaelena.github.io/wallpaper/img/BlackWhite10.jpg'
        }
      ],



      qwert:'привет',
      titleTask: 'Заголовок компонента',
      select:'nohello',
      test: "https://bagira-zoo.club/upload/iblock/2ed/2ed255a8ad64ecd9bd4f95670fbca466.jpg",
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
    toggleMenu(){
      if (this.visibleMenu){
        this.visibleMenu = false
      } else {
        this.visibleMenu = true
      }
    },
    cangeBg(){
     const newIndex = event.target.dataset.index
    //  нужно обновить состояние
    this.currentPageBg = newIndex
    },
    switchModel(){
      this.isShowModel = !this.isShowModel;
    },
    addTask(){
      // Остановить событие
      event.preventDefault();
      // Получить введенный текст
      console.log(this.textNewTask)
      const textInInput = this.textNewTask
      const newObject = {
        title: textInInput
      }
      this.list.push(newObject);
      this.switchModel();
    },
    // вызовем функцию для закрытия окна
    dellTask (index){
      event.preventDefault();
      const newList = this.list.filter((item, indexItem) => {
        return index !== indexItem
        
      })
      // Обновить лист
      this.list = newList
    },
    
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
body{
  margin: 0;
}
.task-list{
  width: 30%;
  min-height: 400px;
  background-color: white;
  padding: 5px

}
.task-list ul{
  
  list-style: none;
  padding: 0;
}
.task-list li{
  text-align: left;
  background-color: rgb(226, 226, 225);
  padding: 5px 15px;
  margin: 15px 30px;
  cursor: pointer;

}
.task-list li:hover{
  outline: solid black;
}
form{
  background-color: white;
  width: 400px;
  height: 300px;
  display: flex;
  justify-content: center;
  align-items: center;
  position: relative;
}
.close{
position: absolute;
top: 3px;
right: 3px;
}
.form-content button {
margin-top: 10px;
}
.overlay{
  position: fixed;
  height: 100vh;
  top: 0;
  right: 0;
  width: 100%;
  background-color: rgba(0, 0, 0, 0.563);
  display: flex;
  justify-content: center;
  align-items: center;

}
.conteiner{
  position: fixed;
  height: 100vh;
  top: 0;
  right: 0;
  width: 100%;
  background-size: cover;
}

.menu{
  position: fixed;
  height: 100vh;
  width: 340px;
  left: -340px;
  transition: 1s;
}

.menu.active{
  left: 0;
  
}

.img-button{
  width: 100%;
  height: 100%;
}
.img-button-conteiner{
 width: 160px;
 height: 90px;
 padding: 0;
}

.img-button img{
  width: 100%;
}

</style>
