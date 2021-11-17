<template>
<div>
  <div><input @input="changeFilter" type="search" v-bind:value="filter" placeholder=Search...></div>
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
table {
	width: 100%;
	border: none;
	margin-bottom: 20px;
	border-collapse: separate;
  text-align: center;
}
table thead th {
	font-weight: bold;

	border: none;
	padding: 10px 15px;
	background: #EDEDED;
	font-size: 1.2rem;
	border-top: 1px solid #ddd;
}
table tr th:first-child, table tr td:first-child {
	border-left: 1px solid #ddd;
}
table tr th:last-child, table tr td:last-child {
	border-right: 1px solid #ddd;
}
table thead tr th:first-child {
	border-radius: 20px 0 0 0;
}
table thead tr th:last-child {
	border-radius: 0 20px 0 0;
}
table tbody td {
	
	border: none;
	padding: 10px 15px;
	font-size: 1rem;
	vertical-align: top;
}
table tbody tr:nth-child(even) {
	background: #F8F8F8;
}
table tbody tr:last-child td{
	border-bottom: 1px solid #ddd;
}
table tbody tr:last-child td:first-child {
	border-radius: 0 0 0 20px;
}
table tbody tr:last-child td:last-child {
	border-radius: 0 0 20px 0;
}

input[type=search] { 
	color: black;  
	text-align: left;
	cursor: pointer;
	display: block; 
  font-size: 1.5rem;
	width: 50%; 
	letter-spacing: 4px;        
	text-shadow: 0 0 2px rgb(85, 70, 70);       
	word-spacing: 20px;      
  margin-top: 2rem; 
  margin-bottom: 2rem; 
  margin-left: 25% ;        
}
</style>
