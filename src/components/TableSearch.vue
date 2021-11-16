<template>
<div>
  <div><input @input="changeFilter" type="text" v-bind:value="filter"></div>
  <div>
    <table>
      <thead>
        <tr>
        <th v-for="field in fieldTable" v-bind:key="field">
          <a href="#" v-on:click="sortBy(field)">
            {{field}}
          </a>
        </th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in valuesTable" :key="item">
          <td v-for="propItem in fieldTable" :key="propItem">{{item[propItem]}}</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>
</template>

<script>
export default {
  props:{
    fieldTable:{
      type:Array,
      required:true
    },
    valuesTable:{
      type:Array,
      required:true
    }
  },
data(){
  return{
    sortKey: '',
    filter:'',
  }
},
methods:{
    sortBy: function(sortKey) {
      this.$emit('sorting',sortKey)
    },
    changeFilter($event){
      this.filter = $event.target.value;
      this.$emit('filtering',this.filter)
    }
}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
