<template>
  <div class="home">
    
    <v-text-field
      @click:append="addTask"
      @keyup.enter="addTask"
      v-model="newTaskTitle"
      class="pa-3"
      outlined
      label ="Add Task"
      append-icon="mdi-plus"
      hide-details
      clearable
      >
    </v-text-field>
   <v-list
      class="pt-0"
      flat
    >

    <div 
        v-for="task in tasks"
       :key="task.id">

       <v-list-item
        @click="doneTask(task.id)"
        :class="{'blue lighten-5' : task.done }"
         >
        <template v-slot:default>
           <v-list-item-action>
               <v-checkbox
                color="primary">
              </v-checkbox>
           </v-list-item-action>

           <v-list-item-content>
               <v-list-item-title
               :class="{'text-decoration-line-through' : task.done }" >
                 {{ task.title }}
               </v-list-item-title>
               <v-list-item-subtitle>
                 {{ task.descr }}
               </v-list-item-subtitle>
               
           </v-list-item-content>
            <v-list-item-action>
               <v-btn
               @click.stop="deleteTask(task.id)"
               icon>
                <v-icon color="red" >mdi-delete</v-icon>
              </v-btn>
        </v-list-item-action>
           
        </template>

      </v-list-item> 
    </div> 
     </v-list>
     
    </div>  
    
</template>

<script>
 

  export default {
  data() {
    return {
      name: 'Todo',
      dialog: false,
      newTaskTitle:'',
      newTaskDescription: '',
      tasks: [
        {
          id: 1,
          title: 'Get bannanas',
          descr: 'bannanas is a fruit',
          done: false,
        },
        {
          id: 2,
          title: 'Get apple',
          descr: 'bannanas is a fruit',
          done: true,
        },
        {
          id: 3,
          title: 'Get bannanas',
          descr: 'bannanas is a fruit',
          done: false,
        },
      ]
    }
  },

  methods: {
     doneTask(id){
      let task = this.tasks.filter(task => task.id == id)[0]
      task.done = !task.done
     },
     deleteTask(id){
       this.tasks = this.tasks.filter(task => task.id !== id)
     },
     addTask() {
       let newTask = {
         id: Date.now(),
         title: this.newTaskTitle,
         descr: this.newTaskDescription,
         done:false
       }
       this.tasks.push(newTask)
       this.newTaskTitle = ''
       this.newTaskDescription = ''
     }
    }
  }

</script>