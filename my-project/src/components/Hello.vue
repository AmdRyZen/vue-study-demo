<template>
 <!--<div class="hello">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <ul>
      <li><a href="https://vuejs.org" target="_blank">Core Docs</a></li>
      <li><a href="https://forum.vuejs.org" target="_blank">Forum</a></li>
      <li><a href="https://gitter.im/vuejs/vue" target="_blank">Gitter Chat</a></li>
      <li><a href="https://twitter.com/vuejs" target="_blank">Twitter</a></li>
      <br>
      <li><a href="http://vuejs-templates.github.io/webpack/" target="_blank">Docs for This Template</a></li>
    </ul>
    <h2>Ecosystem</h2>
    <ul>
      <li><a href="http://router.vuejs.org/" target="_blank">vue-router</a></li>
      <li><a href="http://vuex.vuejs.org/" target="_blank">vuex</a></li>
      <li><a href="http://vue-loader.vuejs.org/" target="_blank">vue-loader</a></li>
      <li><a href="https://github.com/vuejs/awesome-vue" target="_blank">awesome-vue</a></li>
    </ul>
  </div>-->
  <div class="hello">
    <h1>{{msg}}</h1>
    <h2>{{title}}</h2>
    <label for="ip">添加代办事项：<input id="ip" type="text" v-model="newItems" @keyup.enter="addItem"></label>
    <ol>
      <li v-for="item in items" v-bind:class="{Finished:item.isFinished}" v-on:click="toogleFinished(item)">
        {{item.label}}
      </li><br/>
    </ol>
  </div>
</template>

<script>
import Store from '../lib/store.js';
console.log(Store);
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to my first Vue.js App',
      title: 'todolist',
      name:'todolist',
      items:Store.fetch(),
      newItems:''
    }
  },
  watch:{
    items:{
      handler:function(items){
      Store.save(items);
      },
      deep:true
    }
  },
  methods: {
     toogleFinished: function(item) {
       item.isFinished=!item.isFinished;
     },
     addItem:function(){
       this.items.push({
         label:this.newItems,
         isFinished:false
       });
       this.newItems="";
     }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.Finished{
  text-decoration: line-through;
}
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}


a {
  color: #42b983;
}
</style>
