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
          Задание {{index + 1}}. {{ task.title}}
          <button @click="dellTask(index)">Удалить</button>
          <!-- Сделать функцию, которую мы будем открывать в попапе текст и в нем редактировать -->
          <button @click=" changeTask(index)">Редактировать</button>
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
          src:'https://img1.akspic.ru/crops/9/9/4/1/4/141499/141499-priroda-nebo-gora-ledyanaya_forma-prirodnyj_landshaft-7680x4320.jpg'
        },
        {
          id:'fdvffvf',
          src:'https://img3.akspic.ru/crops/0/3/0/8/7/178030/178030-pejzazhnaya_zhivopis-zhivopis-42zapad-voda-oblako-3840x2160.jpg'
        },
        {
          id:'gbffhgnfdh',
          src:'https://img2.akspic.ru/crops/9/9/8/7/7/177899/177899-zakon-grafika-abstraktnoe_iskusstvo-3d_vizualizaciya-art-3840x2160.jpg'
        },
        {
          id:'fdvbdghvf',
          src:'https://img3.akspic.ru/crops/7/2/9/7/7/177927/177927-gora_everest-gora-sammit-gornyj_hrebet-planshet-3840x2160.jpg'
        },
        {
          id:'fdfgdhj',
          src:'https://img3.akspic.ru/crops/2/3/8/6/7/176832/176832-ladon-priroda-rastenie-list-nazemnoe_rastenie-3840x2160.jpg'
        },
        {
          id:'fdfgdhj',
          src:'https://img3.akspic.ru/crops/3/4/3/7/7/177343/177343-sentyabr-rozovyj-materialnoe_svojstvo-art-polutona_i_ottenki-3840x2160.jpg'
        },
        {
          id:'fdfgdshj',
          src:'https://img3.akspic.ru/crops/8/1/0/6/7/176018/176018-prirodnyj_zapovednik_ta_syua-zapadnyj_los_andzheles_buddijskij_hram-oblako-atmosfera-gora-3840x2160.jpg'
        },
        {
          id:'fdfsfdj',
          src:'https://img1.akspic.ru/crops/1/2/2/6/7/176221/176221-apelsin-dizajn-dnevnoe_vremya-priroda-lazurnyj-3840x2160.jpg'
        },
        {
          id:'fdfsdsdj',
          src:'https://img1.akspic.ru/crops/3/3/3/6/7/176333/176333-josemitskij_nacionalnyj_park-nacionalnyj_park-gora-oblako-ekoregion-3840x2160.jpg'
        },
        {
          id:'fdfdsdsdhj',
          src:'https://img3.akspic.ru/crops/4/1/5/6/7/176514/176514-list-melkij_fokus-rastenie-nazemnoe_rastenie-pochvopokrovnaya-3840x2160.jpg'
        }

      ],
         
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
    changeTask (){
      event.preventDefault();
      this.textNewTask = event.title; 
      this.switchModel();
      
      // input.value = this.task.title;
      
      // const newList = this.list.filter((item, index) => {
      //   console.log(e.title)
        
        //return e.title = newTitle
        
      // })
      
      // Обновить лист
      // this.list = newList
    }
    
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
  background-color: rgba(255, 255, 255, 0.533);
  padding: 5px;
  border: 1px solid white;
  border-radius: 10px;

}
.task-list ul{
  
  list-style: none;
  padding: 0;
  color: white;
}
.task-list li{
  text-align: left;
  background-color: rgb(122, 122, 122);
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
