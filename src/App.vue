<template>
  <div id="app">

    <header class="header">
      <h1>TODO-LIST</h1>
      <input v-model="inputValue" @keyup.enter="add" autofocus="autofocus" autocomplete="off" placeholder="写、东西" class="todolist-input">
    </header>

    <section class="main">
      <ul class="todo-list">
        <li class="todo" v-for="(item,index) in list" >
          <div class="view">
            <span class="index"> &nbsp; &nbsp;{{ index+1 }} . </span>
            <label>{{ item }}</label>
            <button class="destroy" @click="remove(index)">
              ×
            </button>           
          </div>
        </li>
      </ul>
    </section>

    <footer class="footer" v-if="list.length!=0">
      <span class="todo-count" >
        共<strong>  {{ list.length }} </strong> 条 待实施
      </span>

      <button class="destroy-all" @click="clear">
        清空
      </button>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'App',
  data(){
    return{
      list:[],
      inputValue:""
    }
  },
  methods:{
    add:function(){
      if(this.inputValue==""){
        alert('不能什么都不写哦');
      }else{
      this.list.push(this.inputValue);
      this.inputValue=""; 
      /*storage.set('list',this.list);*/
      localStorage.setItem('list',JSON.stringify(this.list));
      }
     
    },
    remove:function(index){
      /*console.log('index');*/
      this.list.splice(index,1);
      /*storage.set('list',this.list);*/
      localStorage.setItem('list',JSON.stringify(this.list));
    },
    clear:function(){
      this.list=[];
      /*storage.set('list',this.list);*/
      localStorage.setItem('list',JSON.stringify(this.list));
    }
  },
  mounted(){
    /*var list=storage.get('list');*/
    var list=JSON.parse(localStorage.getItem('list'));
    this.list=list;
  }
}
</script>

<style>
html{
  background-color: #eee;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  box-sizing: border-box;
}
input{
  width: 500px;
  height: 40px;
  position: relative;
  display:block;
  margin: 0 auto;
  border:1px solid #ccc;

}
.header{
  position: relative;
  margin: 0 auto;
}
.main{
  position: relative;
  /*margin:0 auto;*/
  margin-top: 10px;


}
.todo-list{
  width: 500px;
  margin:0 auto;
  list-style: none;
  padding-left: 0px;
 /* box-shadow: 10px 10px 5px #888;*/
}
.todo{
  height: 50px;
  list-style: none;
  line-height: 50px;
  width: 100%;
  background-color: white;
  border-bottom: 1px solid #ccc;
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;
  text-align: left;
}
.destroy{
  float: right;
  border: 0;
  background-color: transparent;
  outline: none;
  font-size: 20px;
  margin-top: 13px;
  display: none;
}
.destroy-all{
  float: right;
  border: 0;
  background-color: transparent;
  font-size: 16px;
}
.todo:hover .destroy{
  display: block;
}
.footer{
  position: relative;
  height: 36px;
  width: 488px;
  padding-top: 10px;
  padding-left:10px;
  margin:0 auto;
  background-color: white;
  border-bottom: 1px solid #ccc;
  border-left: 1px solid #ccc;
  border-right: 1px solid #ccc;

}
.todo-count{
  float: left;
}
.destroy-all{
  float: right;
}
</style>

