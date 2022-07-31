<template>
  <div class="home">
    <v-text-field
            @click:append="addTodo()"
            @keyup.enter="addTodo()"
            clearable
            class="pa-3"
            label="Add todo"
            append-icon="mdi-plus"
            hide-details v-model="newTask.title" 
          ></v-text-field>
    <v-list flat class="pt-0">

      <div
      v-for="task in tasks"
         v-bind:key="task.id"
      >
        <v-list-item
        @click="completedTodo(task.id)"
        :class="{ 'blue lighten-5': task.complete}">
          <template v-slot:default>
            <v-list-item-action>
              <v-checkbox
                :input-value="task.complete"
                color="primary" 
              ></v-checkbox>
            </v-list-item-action>

            <v-list-item-content>
              <v-list-item-title :class="{'text-decoration-line-through': task.complete}">
                {{task.title}}
                </v-list-item-title>
            </v-list-item-content>
           <v-list-item-action>
          <v-btn icon @click.stop="deleteTask(task.id)">
            <v-icon color="primary lighten-2">mdi-delete</v-icon>
          </v-btn>
        </v-list-item-action>
          </template>
          

        </v-list-item>
        <v-divider></v-divider>
        </div>
 </v-list>
       
  </div>
</template>

<script>

  export default {
    name: 'Todo',
    data () {
      return{
        newTask: {
          title: "",
        },
        tasks: [
          // {
          //   id: 1,
          //   title: 'Groceries',
          //   complete: false,
          // },
          // {
          //   id: 2,
          //   title: 'Laundry',
          //   complete: false,
          // },
          // {
          //   id: 3,
          //   title: 'Hackerrank',
          //   complete: false,
          // },
        ]
      }
    },
    components: {
    },
    methods: {
      completedTodo(id){
        let task = this.tasks.filter(x => 
          x.id == id
        )[0]
        task.complete = !task.complete
      },
      deleteTask(id){
        this.tasks = this.tasks.filter(task => task.id != id)
      },
      addTodo(){
        let newTodo = {
          id: Date.now(),
          title: this.newTask.title,
          complete: false,
        }
        this.tasks.push(newTodo)
        this.newTask.title = '';
      }
    }
  }
</script>
