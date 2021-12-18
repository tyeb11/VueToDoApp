<template>
<div class="container">

    <h1>To Do List</h1>

    <form @submit="onSubmit()">
      
      <input v-model="todovalue" placeholder="ToDo">
      <button>Submit</button>

    </form>
    <ul>
      <li v-for="(todo,index) in todolist" :key="index" @click="tododone(todo)"
      :class="{done:todo.done}">
        {{todo.content}}
        
        <button @click="removedata(index)">X</button>
      </li>
    </ul>

</div>
  
  
</template>

<script>
import { ref } from 'vue';



export default {

  setup(){
    const todovalue = ref('');

    const defaultData=[{
      done:false,
      content:"Welcome"
    }]

    const tododata = JSON.parse(localStorage.getItem('todolist')) || defaultData;
    const todolist =ref(tododata);

   function onSubmit(){
     if(todovalue.value){
       todolist.value.push({
         done:false,
         content:todovalue.value
       })
       todovalue.value ='';

     }
     savedata();

    }
    function savedata(){
      const data = JSON.stringify(todolist.value)
      localStorage.setItem('todolist',data)
    }
    function removedata(index){
      todolist.value.splice(index,1);
      savedata();
    }
    function tododone(todo){
      todo.done=!todo.done
      savedata()
    }



    return{
      todovalue,
      todolist,
      onSubmit,
      removedata,
      savedata,
      tododone
    }
  }

}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Indie+Flower&display=swap');
body{
  background: whitesmoke;
  
}
.container{
  
  max-width: 600px;
  
  border-radius: 10px;
  margin-left: auto;
  margin-right: auto;
  margin-top: 50px;
}
h1{
  text-align: center;
  font-weight: bold;
  font-size: 50px;
  font-family: 'Indie Flower',cursive;

}
form{
  display: flex;
  flex-direction: column;
  width: 100%;
  
}
form button{
  cursor: pointer;
      height: 48px;
			background-color: black;
			
			color: white;
			font-weight: bold;
			outline: none;
			border-radius: 6px;
      
				box-shadow: none;
				outline: none;
				padding-left: 12px;
				padding-right: 12px;
				border-radius: 6px;
				font-size: 18px;
				margin-top: 40px;
				margin-bottom: 12px;
}
input{
  cursor: pointer;
  border: none;
  border-bottom:1px solid rgba(0, 0, 0, 0.2)  ;
  
			background-color: transparent;
			outline: none;
			
			color: black;
			font-weight: bold;
			
      box-shadow: none;
      
      height: 48px;
				box-shadow: none;
				outline: none;
				padding-left: 12px;
				padding-right: 12px;
				
				font-size: 25px;
				margin-top: 22px;
				margin-bottom: 12px;

}
ul{
  padding: 60px;
}
li{
  display: flex;
    align-items: center;
    justify-content: space-between;
    background: whitesmoke;;
    border: 1px solid black;
    margin: 5px;
    padding: 20px 20px;
    cursor: pointer;
    font-weight: bold;
    font-size: 25px;
    overflow: auto;
  

}

li button{
  background-color:whitesmoke;
    color: black;
    border: 5px solid whitesmoke;
    cursor: pointer;
    
}
.done{
  text-decoration: line-through;
  text-decoration-color: red;
}

</style>
