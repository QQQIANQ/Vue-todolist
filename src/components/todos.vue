<template>

  <div class="todos">
      <h1>Here is the Todolist of sacré Qian</h1>

    <TodoComponent>

    </TodoComponent>


  </div>

</template>


<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';
  import TodoComponent from '../components/todo.vue';

  @Component(
      {
        components: {
          TodoComponent
        }
  }
  )
  export default class TodosComponent extends Vue {



  }


</script>

