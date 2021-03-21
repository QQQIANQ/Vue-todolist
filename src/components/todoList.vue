<template>
  <div class="todo-list">
    <h3>Here is the TodoList of sacré Qian</h3>
    <div class="input-group mb-6">
      <input type="text" class="form-control"
             placeholder="Todo" aria-label="Todo" aria-describedby="button-addon2"
      v-model="todoInput">
      <button class="btn btn-outline-secondary" type="button" id="button-addon2"
              @click="addTodo">
        ADD to List
      </button>
      <button type="button" class="btn btn-danger"
      @click="delAll" >Clear</button>

    </div>
    <ul class="list-group">
      <li v-for="(todo,index) in todoList"
          :key="index"
          :class="{
            'list-group-item' :true,
            'list-group-item-secondary': todo.checked
          }"
      @click="todo.toggleChecked();countTodo()" >
        <div v-if="index == cursor_id">
        <input type="text" v-model.trim="todo.todo" @keyup.enter="edited(index,todo)" @blur="edited(index,todo)" />
        </div>
        <div v-else @dblclick="editing(index,todo)">
          {{todo.todo}}
          <button type="button" class="btn-close" style="float:right" aria-label="Close"
                  @click.stop="delTodo(todo)"></button>
        </div>

      </li>
    </ul>
    <div class="card-footer text-muted">
      <div v-if="restTodo>0"> There are {{restTodo}} things are waiting for you ! {{ count }} done</div>
    </div>
    </div>
</template>
<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';

  class Todo{
    todo ='';
    checked = false;

    constructor(todo:string) {
      this.todo = todo
      this.checked = false
    }

      toggleChecked(){
      this.checked=!this.checked
      }

  }

  @Component({
  })
  export default class TodoListComponent extends Vue {

    todoInput ='';
    cursor_id = null
    todoList: Todo[] = [];
    restTodo = this.todoList.length;
    count = 0

    addTodo():void{
      let todo = new Todo(this.todoInput)
      this.todoList.push(todo)
      this.restTodo = this.todoList.length
    }
    delTodo(todo:Todo):void{
      this.todoList = this.todoList.filter((todoItem) => {
        return todoItem !== todo;
      })
      this.restTodo = this.todoList.length
    }

    countTodo(){
      var done = 0
      for (let todo of this.todoList) {
        if(todo.checked){
          done++
        }
      }
      this.count = done
    }

    delAll():void{
      this.todoList=[]
      this.restTodo = this.todoList.length
      this.count = 0
    }
    editing(i: null,todo:Todo):void{
      this.cursor_id=i
      this.todoInput = todo.todo
    }
    edited(i: string,todo:Todo):void{
      this.cursor_id = null;
      this.todoList[parseInt(i)] = todo
    }

    mounted():void{
      this.todoList.push(new Todo('Qian'))
      this.todoList.push(new Todo('est un génie'))
      this.restTodo = this.todoList.length

    }
    
  }

</script>

<style scoped>


.list-group-item-secondary{
  text-decoration: line-through;
}



</style>
