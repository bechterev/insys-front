<template>
  <TableSearch v-bind:fieldTable="generateFields()" v-bind:valuesTable="generateUsers()" @filtering="updateListValues" @sorting="sortBy" />
</template>

<script>
import TableSearch from "./components/TableSearch.vue";
import axios from "axios";

export default {
  name: "App",
  data(){
    return{    
      urlByAllUsers:'http://localhost:5000/user/all?page=1',
    datas:[{}],
   filteringData:[],
   reverse:false,
   sortKey:''}
  },
  components: {
    TableSearch,
  },
  methods:{
      generateFields:function(){
   return  ["id","fio","gender","birthday"];
  },
        generateUsers:function(){
   return  this.filteringData;
  },
  updateListValues:function(str){
    str.trim();
    if(str!=""){    
    let search = new RegExp(`.*${str}.*`,'gi')
    this.filteringData = this.datas.filter(el=>
    {
      if( Object.values(el)
      .filter(x=>{if(x!==null&&search.test(x.toString())){ 
        return x;
      }}
      ).length>0)
      {   
        return el;
      }
    })}
    else {this.filteringData = this.datas;}
  },
      sortBy: function(sortKey) {
      this.reverse = (this.sortKey == sortKey) ? !this.reverse : false;
      this.sortKey = sortKey;
      if(this.reverse){
        this.filteringData.sort((prev, next) => {
         if ( prev[this.sortKey] < next[this.sortKey] ) return -1;
         if ( prev[this.sortKey] < next[this.sortKey] ) return 1;
        });
      }
      else{
                this.filteringData.sort((prev, next) => {
         if ( prev[this.sortKey] > next[this.sortKey] ) return -1;
         if ( prev[this.sortKey] > next[this.sortKey] ) return 1;
        });
      }
    },
    async fetchUser(){
      try{
        const result = await axios.get(this.urlByAllUsers);
        this.datas = result.data;
        return result.data;
      }
      catch(e){
        console.log('error: users not found',e)
      }
    }
  },
      mounted(){
     this.fetchUser().then(val=>{this.filteringData=[...val]})

    }
}; 
</script>

<style>
#app {

}
</style>
