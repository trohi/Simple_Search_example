<template>
  <div id="app">
    <input v-model="search" >
    <div  v-for="(item, index) in filteredP" v-bind:key="index" >
     <h2>Name: {{item.Name}}</h2>
     <h2>Pice: {{item.Price | rounding}}</h2>
     <hr>
      </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import axios from "axios"

export default {
  name: 'App',
  data(){
    return{
      items:[],
      search:"",
    }
  },
  components: {
    HelloWorld
  },
  methods:{
    getUrl(){
      axios.get("https://output.jsbin.com/jahiwibisi.json")
      .then((res)=>{
        this.items = res.data
        })
    }
  },
  computed:{
    filteredP(){
      return this.items.filter((item)=>{
        return item.Name.indexOf(this.search) > -1
      })
    }
  },
  filters:{
    rounding(item){
     return item.toFixed(2)
    }
  },
  created(){
    this.getUrl()
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
