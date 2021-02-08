
<template>
  <div id="app" >
   <br>
    
    <div class="header"> TO-DO List </div>
    
    <br>
    <!-- Field to type in todos -->
    <input v-model="newtodo" id="Inputfield" type="text" class="textbox" placeholder="Write your task here"/>
     <br>
  
      <br>
      <!-- Addbutton to add typed todo to list -->
    <button v-on:click="addNewTodo" id="add" class="btn" > Add task</button>


  <br>
 <br>
 <!-- Header for not finished task list -->
 <div class="subheader">Not finished tasks</div>

<!-- todo list -->
<ul> 
  <li v-for="(nftodo, id) in nftodos" v-bind:key="nftodo" class="notfinishedTasks">
    <!-- Checkbox at the beginning of every todo -->
   <input type="checkbox" v-on:change="addfTask(nftodo, id)" /> 
     <!-- Todos  -->
    <span class="todo">
        {{nftodo.title}} 
    </span>
     <!-- X Button at the end of every todo -->
     <span @click="removetask(id)" class="removebutton" >x</span>
  </li>
</ul>


 <!-- Header for finished task list -->
<div class="subheader">Finished tasks</div>

<!--  finished todo list  -->
<ul>
  <li v-for="(ftodo, id) in ftodos" v-bind:key="ftodo" class="finishedTasks">
    <!-- Checkbox at the beginning of every finished todo -->
   <input type="checkbox" checked v-on:change="unfinishTask(ftodo, id)" /> 
   <!-- finished todos -->
   <span class="done">   
      {{ftodo.title}}
    </span>
     <!-- X Button at the end of every finished todo -->
    <span @click="removefinishedtask(id)" class="removebutton">x</span>
  </li>
</ul>


</div>
</template>

<script>


export default {
  name: 'app',
  data: () => ({
//array for finished todos
ftodos:[],

//array for not finished todos
nftodos: [],
  }),

methods: {
  // method to add the typed todo to the not finished list
    addNewTodo: function () {
    
      this.nftodos.push({
           
        title: this.newtodo
      })
    // clears inputlist
    this.newtodo ="";
    },

  // delete finished task from not finished list and add it to finished list
    addfTask: function (finishedtodo, id) {
    
     this.ftodos.push({
      
        title: finishedtodo.title        
        
      })
       this.$delete(this.nftodos, id);
    },

  // delete not finished task from finished list and add it to not finished list
    unfinishTask: function (notfinishedtodo, id) {
    
     this.nftodos.push({
      
        title: notfinishedtodo.title        
        
      })
       this.$delete(this.ftodos, id);
    },
  // delete task from not finished tasks list
    removetask: function (id) {
      this.$delete(this.nftodos, id);
    },

  // delete task from finished tasks list
    removefinishedtask: function (id){
      this.$delete(this.ftodos, id);
    }
  } 
}
</script>


<style>

/* style for "Add task" button  */
.btn{
  background-color: #20bd43;
  border: 0; 
  border-radius: 30px; 
  color: white;
  size:180px;
  width: 80px;
  height: 20px;
  text-align:center;
}

/* style for todo list header  */
.header{
  color: #a6a6a6;
  text-align: center;
}

/* style for header of task lists  */
.subheader{
  font-size: 12px;
  text-align: left;
  margin-left: 40px;
  color: #a6a6a6;
}

/* style for textfield  */
.textbox{  
border-width: 0px;
border-radius: 3pt; 
box-shadow: 2px 2px 2px #a6a6a6;
}

/* style for placeholder in textfield  */
::placeholder {
  color: #a6a6a6;
  opacity: 1; 
}

/* style for not finished Tasks  */
.notfinishedTasks{
  list-style-type: none; 
  font-size: 10px;  
  text-align: left; 
  border-width: 0px; 
  box-shadow: 2px 2px 2px #a6a6a6;
  width: 170px;
  color: black;
  margin-top: 2pt;
}

/* style for finished Tasks  */
.finishedTasks {
  text-decoration: line-through;
  list-style-type: none; 
  font-size: 10px; 
  text-align: left; 
   border-width: 0px; 
  box-shadow: 2px 2px 2px #a6a6a6;
  width: 170px;
  color: #a6a6a6;
  margin-top: 2pt;  
} 

/* style for text of todos  */
.todo{
 position:absolute;
 size: 100%;
 transform:translateY(20%);
 font-size: 12px;
}

/* style for text of finished todos  */
.done{
 text-decoration: line-through;
 position:absolute;
 size: 100%;
 transform:translateY(20%);
 font-size: 12px;
}

/* style for "x" button  */
.removebutton{
 position:absolute;
 size: 100%;
 transform:translateY(20%);
 transform: translateX(1850%);
 font-size: 15px;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #a6a6a6;
  margin-top: 60px;
  width: 250px; 
  text-align: center;
}

  
</style>