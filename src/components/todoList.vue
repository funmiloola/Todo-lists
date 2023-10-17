<template>
  <div id="todo">
  <main>
  <header>
  <h1>T O D O</h1>
  <img src="@/assets/images/icon-moon.svg" alt="theme-icon">
  </header>
  <section>
  <input type="text" id="add-todo" placeholder="Create a new todo..."   v-model="newTodo"  @keyup.enter="addTodo">
  <article>
  <ul>
  <li v-for="(list, index) in lists" :key="index">
  <div class="todo-details">
    <input type="checkbox" id="option1" name="options" v-model="list.isChecked" />
    <label for="option1" :class="{ 'cancelled': list.isChecked }">{{ list.label }}</label>
  </div>
  <img src="@/assets/images/icon-cross.svg" alt="delete-icon" id="icon-delete" v-on:click="deleteTodo(index)">
  </li>
  </ul>
  <div id="footer">
   <p id="todo-left">{{ quantity() }} items left</p>
   <div class="filtering">
   <p v-on:click="showAll">All</p>
   <p v-on:click="incompleteTodo">Active</p>
   <p v-on:click="completedTodo">Completed</p>
   </div>
   <p id="todo-cleared" v-on:click="clearCompleted">Clear Completed</p>
  </div>
  </article>
  </section>
  <div class="filteriing">
   <p v-on:click="showAll">All</p>
   <p v-on:click="incompleteTodo">Active</p>
   <p v-on:click="completedTodo">Completed</p>
   </div>
  </main>
  </div>
</template>

<script>

export default {
  components: {
   
  },
  data(){
    return{
    lists:[
     { label:'Complete online Javascript course', icon:'@/assets/images/icon-cross.svg', isChecked:false,},
     { label:'Jog around the park 3x', icon:'@/assets/images/icon-cross.svg', isChecked:false,},
     { label:'10 minutes meditation',  icon:'@/assets/images/icon-cross.svg',isChecked:false,},
     { label:'Read for 1 hour', icon:'@/assets/images/icon-cross.svg', isChecked:false,},
     { label:'Pick up groceries', icon:'@/assets/images/icon-cross.svg', isChecked:false,},
     { label:'Complete Todo App on Frontend Mentor', icon:'@/assets/images/icon-cross.svg', isChecked:false,}
     ],
     newTodo:'', 
     completedTodo:false,
     incompleteTodo:false,
    }
    },
    methods: {
     quantity() {
  return this.lists.filter((list) => !list.isChecked).length;
     },
     addTodo(){
     if(this.newTodo.trim()!==''){
     this.lists.push({
     label:this.newTodo,
     completed:false,
     });
     this.newTodo = '';
    }
    },
    deleteTodo(index){
    this.lists.splice(index, 1);
    },
    showAll(){
    return this.lists
    },
    completedTodo(){
    this.lists = this.lists.filter((list) => list.isChecked);
    },
    incompleteTodo(){
    this.lists = this.lists.filter((list) => !list.isChecked);
    },
    clearCompleted(){
    this.lists = this.lists.filter((list) => !list.isChecked);
    }
  
  
}
  
}
</script>
 
<style scoped>
#todo{
  font-family:Josefin Sans;
  }
 header{
   margin:0;
   align-items:center;
   display:flex;
   justify-content:space-between;
 }
 main{
   position:absolute;
   left:37%;
   top:100px;
   }
@media(max-width:768px){
   main{
    left:10%;
    top:60px;
    }
  }
h1{
 color:white;
 }
#add-todo{
  margin-bottom:0.5rem;
  padding-left:32px;
  padding-right:280px;
  padding-top:10px;
  padding-bottom:10px;
  border-radius:2px;
  border:none;
  }
  @media(max-width:768px){
   #add-todo{
   padding-bottom:1rem;
   padding-top:1rem;
   }
   }
input[type="checkbox"] {
  appearance: none;
  width: 20px;
  height: 20px;
  border: 1px solid hsl(236, 33%, 92%);
  border-radius: 50%;
  cursor: pointer;
}

input[type="checkbox"]:checked {
  background-image:url('@/assets/images/icon-check.svg');
  
  background-color:blue;
}

 
input::placeholder{
   color:hsl(236, 9%, 61%);
   }
.cancelled{
  text-decoration:line-through;
  color:hsl(234, 39%, 85%);
  }
article{
   background:white;
   margin-top:1rem;
   box-shadow:0px 0px 2px hsl(234, 11%, 52%);
   }
li{
  position:relative;
  list-style-type:none;
  margin-left:-2.5rem;
  padding-bottom:0.7rem;
  padding-top:0.7rem;
  border-bottom:1px solid  hsl(236, 33%, 92%);
  color:hsl(235, 19%, 35%);
  font-size:14px;
  }
 @media(max-width:768px){
  li {
  padding-bottom:1.2rem;
  padding-top:1.2rem;
  }
  }
 .todo-details{
       display:flex;
       gap:10px;
       align-items:center;
    }
#icon-delete{
    left:28rem;
    position:absolute;
    top:0.8rem;
    width:16px;
}
#footer{
   display:flex;
   gap:70px;
   padding-left:10px;
   margin-top:-1.2rem;
   font-size:14px;
   }
.filtering{
 display:flex;
 gap:8px;
 color:hsl(234, 11%, 52%);
 cursor:pointer;
 }
 @media(max-width:768px){
  .filtering{
   visibility:hidden;
   }
 }
 #todo-left{
   color:hsl(234, 39%, 85%);
   }
#todo-cleared{
 color:hsl(234, 39%, 85%);
 cursor:pointer;
 }
p:active{
  color:blue;
  }
.filteriing{
  display:flex;
  justify-content:center;
  gap:18px;
  align-items:center;
  color:hsl(234, 11%, 52%);
  cursor:pointer;
  padding-left:2rem;
  visibility:hidden;
  background:white;
  margin-top:1rem;
  box-shadow:0px 0px 2px hsl(234, 11%, 52%);
}
@media(max-width:768px){
  .filteriing{ 
    visibility:visible;
    }
  }
</style>
