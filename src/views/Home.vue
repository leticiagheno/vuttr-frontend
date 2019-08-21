<template>
  <div class="home">
    <h1 id="page-title"> VUTTR </h1> 
    <h2 id="page-subtitle"> Very Useful Tools To Remember </h2> 
    <div>
    <input id="search-item" type="search" placeholder="Digite o que está procurando..."/>
    <input id="tags-check" type="checkbox"/> Search in tags only
    <button> </button>
    </div>
    <div
      v-for="tool in results" :key="tool.id" >
      <Card :tool="tool"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Card from "@/components/Card.vue";
import axios from 'axios';

export default {

  name: "home-page",
  components: {
    Card
  },
  data () {
    return {
      results: []
    }
  },
  beforeMount() {
    var vm = this;
    axios
    .get('http://localhost:3000/tools')
    .then(response => {vm.results = response.data.result})
  }
};
</script>

<style scoped>

#page-title {
  text-align: left;
  font: Semibold 42px/50px Source Sans Pro;
  letter-spacing: 0.84px;
  color: #170C3A;
  opacity: 1;
}

#page-subtitle {
  text-align: left;
  font: Semibold 36px/40px Source Sans Pro;
  letter-spacing: 0.72px;
  color: #170C3A;
  opacity: 1;
}

#search-item {
  background: #F5F4F6 0% 0% no-repeat padding-box;
  border: 1px solid #EBEAED;
  border-radius: 5px;
  opacity: 1;
  width: 403px;
  height: 50px;
}

</style>
