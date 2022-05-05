<template>
 <div class="container">
    <!-- Heading -->
    <h2 class="text-center mt-5">Todo App</h2>

    <!-- Input -->
    <div class="d-flex mt-5">
      <input v-model="task" type="text" placeholder="Enter your task here.." class="form-control" />
      <button @click="addTask" class="btn btn-warning rounded-0">
        ADD
      </button>
    </div>
    <!-- Task Table -->
    <table class="table table-bordered mt-5">
  <thead>
    <tr>
      <th scope="col">Task</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">Edit</th>
      <th scope="col" class="text-center">Delete</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <td>
        <span :class="{'finished': task.status == 'finished' }">
          {{task.name}}
        </span>
      </td>
      <td style="width:120px"><span @click="changeStatus(index)" class="pointer" :class="{'text-danger': task.status == 'to-do', 'text-warning': task.status == 'in-progress', 'text-success': task.status == 'finished'}">{{firstCharUpper(task.status)}}</span></td>
      <td style="width:120px">
        <div @click="editTask(index)" class="text-center">
          <span class="fa fa-pen"></span>
        </div>
      </td>
      <td style="width:120px">
        <div @click="deleteTask(index)" class="text-center">
          <span class="fa fa-trash"></span>
        </div>
      </td>
    </tr>
  </tbody>
</table>
    </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task:'',
      editedTask: null,
      statusTask: ['to-do', 'in-progress', 'finished'],
      tasks:[
        {
        name: 'task 1',
        status: 'to-do'
      },
      {
        name: 'task 2',
        status: 'to-do'
      },
      ]
    }
  },

  methods: {
    addTask(){
      if(this.task.length==0) return;
      if(this.editedTask == null){

      this.tasks.push({
        name: this.task,
        status: 'to-do'
      });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task='';
    },

    deleteTask(index){
      this.tasks.splice(index,1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index){
      let newIndex = this.statusTask.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex =0;  
      this.tasks[index].status = this.statusTask[newIndex];  
    },

    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
};
</script>

<style scoped>
.pointer{
  cursor: pointer;
}

.finished{
  text-decoration: line-through;
}
</style>