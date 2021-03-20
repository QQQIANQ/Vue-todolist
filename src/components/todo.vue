<template>
  <div class="todo"> 
    <input v-model="newtask" placeholder="Add une tache!">
    <button v-on:click="addTache(newtask)">
      Add
    </button>

    <button v-on:click="removeAllTaches()">
      Remove All
    </button>
    <ul id = "taches" v-if ="taches.length>1">
      <li  v-for="tache in taches"  :key="tache.message" >
        {{tache.message}}
        <button v-on:click="removeTache()" >
          <i class="bi bi-x">X</i>
        </button>
      </li>

    </ul>

    <footer>
      <span>Il me reste {{ nombreTaches }} taches à faire</span>
    </footer>
  </div>
</template>
<script lang="ts">
  import Vue from 'vue';
  import Component from 'vue-class-component';

  @Component({})
  export default class TodoComponent extends Vue {
    newtask = ''
    taches= [{}]
    nombreTaches = this.taches.length
    addTache(tach:string){

      this.taches.push({message:tach})
      this.nombreTaches=this.taches.length

    }

    removeTache(){
      this.taches.pop()
      this.nombreTaches=this.taches.length
    }

    removeAllTaches(){
      this.taches=[]
      this.nombreTaches=this.taches.length
    }
    
  }

</script>

