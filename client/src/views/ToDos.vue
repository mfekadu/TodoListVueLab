<style scoped>
.table { display: table; }
.row { display: table-row; }
.cell {
  display: table-cell;
  background-color: red;
  padding:20; /* padding is inside the "box" */
  margin:50; /* margin is outside the "box" */
  border-style: solid;
  border-color: black;
}

h1 {
  padding:10px;
  padding-left: 10px;
  /* margin:10px; */
  background-color: green;
  font-size: 15px;
  font-weight: bold;
}
</style>


<template>
    <div class="todos" style="margin-left: 20px">
        <h1> HI FROM TODOS </h1>
        <!-- <h1> My Todo List </h1> -->
        <!-- this is now a data driven component
                that outputs anything in the todos array -->
        <div v-for="(todo, index) in mytodos" v-bind:key="index">
            <div class="table">
                <div class="row">
                    <div class="cell col1">
                    <input type="checkbox" name="name1" id="1"><br>
                    </div>
                    <div class="cell col2"> <span>{{ todo.name }}</span> </div>
                    <div class="cell col3">
                        <span>{{ (todo.duedate) ? todo.duedate : "_".repeat(24) }}</span>
                    </div>
                    <div class="cell col4">
                        <button type="button" name="btn-delete">Delete</button>
                    </div>
                </div>
                </div>

        </div>
        <br>
        <div>
            <h1> ADD NEW TODO </h1> 
            Item name: <input type="text" v-model="item.name"/>
            <br>
            Item Due Date: <input type="text" v-model="item.duedate"/>
            <br>
            <button class="button" v-on:click="addTodoItem">Add</button>
        </div>
    </div>
</template>



<script lang='ts'>
import Vue from "vue";
import { Component } from "vue-property-decorator";

/* NOTE: it is useful for only Api and Client 
 * in separate windows with VS Code */

/* this is creating a component */
@Component
// if default then
// import ToDos from './views/ToDos.vue'
//  if not default then
// import { ToDos } from './views/ToDos.vue'

// NOTE: do npm run serve in the client dir to compile
export default class ToDos extends Vue {
  // this export says, if another files imports this file,
  // then it only gets this component
  mytodos: ToDo[] = [
    { name: "Tod one", duedate: undefined },
    { name: "Tod two", duedate: undefined },
    { name: "Tod three", duedate: new Date() }
  ];
  item: ToDo = {
    name: "",
    duedate: undefined
  };
  addTodoItem() {
    console.log(this.mytodos);
    if (this.item.name === "") {
      return alert("please enter an item name at least");
    }
    this.mytodos.push({ name: this.item.name, duedate: this.item.duedate });
  }
}

interface ToDo {
  name: string;
  duedate: Date | undefined;
}
</script>
