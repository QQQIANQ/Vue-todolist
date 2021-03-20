<template>
  <div class="home">
    <TodosComponent> Todos </TodosComponent>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import {Background} from '../directives/background.directive'
import TodosComponent from '../components/todos.vue'


@Component({
  components: {
    TodosComponent
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
