<template>
  <TableSearch v-bind:fieldTable="generateFields()" v-bind:valuesTable="generateUsers()" @filtering="updateListValues" @sorting="sortBy" />
</template>

<script>
import TableSearch from "./components/TableSearch.vue";

export default {
  name: "App",
  data(){
    return{    
    datas:[{id:1,fio:'ivan ogly',birthday:'1985-03-05',gender:true},
   {id:2,fio:'Petr Mensh',birthday:'1980-12-01',gender:true},
   {id:8,fio:'Ella Gudrick',birthday:'1961-08-22',gender:false},
   {id:10,fio:'Zoe Melnik',birthday:'1992-06-27',gender:false}],
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
    let search = new RegExp(`.*${str}.*`,'gi')
    this.filteringData = this.datas.filter(el=>
    {
      if( Object.values(el)
      .filter(x=>{if(search.test(x.toString())){ 
        return x;
      }}
      ).length>0)
      {   
        return el;
      }
    })
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
    }
  }
}; 
</script>

<style>
#app {

}
</style>
