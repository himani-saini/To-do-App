<template>
  <div class="wrapper text-center mt-5">
    <h1>To-do list</h1>
  
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="input-group mb-3">
          <input v-model="task" type="text" class="form-control" placeholder="Enter task">
          <div class="input-group-append">
            <button class="btn btn-outline-danger" type="button" @click="addTask()">Add</button>
          </div>
        </div>
      </div>
    </div>

  
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="table-container">
          <table class="table table-bordered mt-5">
            <thead>
              <tr>
                <th scope="col">Task</th>
                <th scope="col">Status</th>
                <th scope="col">#</th>
                <th scope="col">#</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(task, index) in tasks" :key="index">
                <td :class="{ completed: task.complete }">{{ task.name }}</td>
                <td><input type="checkbox" v-model="task.complete"></td>
                <td><button class="btn btn-warning" @click="editTask(index)">Edit</button></td>
                <td><button class="btn btn-danger" @click="deleteTask(index)">Remove</button></td>
              </tr>
            </tbody>
          </table>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
export default {
 name: 'HelloWorld',
 props: {
   msg: String
 },

 data() {
   return {
     task:"",
     editedTask: null,
     tasks:[
       {
         name:'Buy a notebook',
         complete:false
       },
       {
         name:'get a pen',
         complete:false
       }
     ]
   }
 },

 computed:{
    isComplete(){
      return this.tasks.filter(task => task.completed).length;
    }
 },

 methods: {
   addTask(){
    if(this.task.length === 0) return;

    if(this.editedTask === null){
     this.tasks.push({
       name: this.task,
       complete:false
     });
    }else{
     this.tasks[this.editedTask].name= this.task;
     this.editedTask=null;
    }
    
     this.task="";
    
   },

   deleteTask(index){
        this.tasks.splice(index,1);
   },

   editTask(index){
     this.task = this.tasks[index].name;
     this.editedTask = index;
   }


 },


}
</script>

<style lang="scss">
@import "src/assets/to-do.scss";
.table-container {
  width: calc(100% - 30px); 
  max-width: 600px; 
  margin: 0 auto; 
}
</style>
