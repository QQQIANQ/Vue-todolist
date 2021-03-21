<template>
  <div class="home">
    <TodoListComponent> Todos </TodoListComponent>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import {Background} from '../directives/background.directive'
import TodoListComponent from '../components/todoList.vue'


@Component({
  components: {
    TodoListComponent
  },
  directives:{
    Background
  }
})
export default class Home extends Vue {

  message= 'test';
  visible = true;
  foo(){
    this.visible = !this.visible;
  }
}
</script>
