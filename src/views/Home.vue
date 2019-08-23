<template>
  <div class="home align-items-center">
    <h1 id="page-title"> VUTTR </h1> 
    <h3 id="page-subtitle"> Very Useful Tools To Remember </h3> 
    <div class="row justify-content-between display-flex ">
    <div class="row col-8 align-items-center">
    <input id="search-item" type="search" class="col-6" placeholder="Digite o que está procurando..."/>
    <input id="tags-check" class="col-1" type="checkbox"/> Search in tags only
    </div>
    <div class="col-4">
      <button class="col-4 align-self-end"  @click="showModal()" > Add </button>
    </div>
    </div>
    <div
      v-for="tool in results" :key="tool.id" >
      <Card :tool="tool"/>
    </div>
  <ToolModal
      v-show="isModalVisible"
      @close="closeModal"
  />
  </div>
</template>

<script>
// @ is an alias to /src
import Card from "@/components/Card.vue";
import ToolModal from '@/components/ToolModal.vue';
import axios from 'axios';

export default {

  name: "home-page",
  components: {
    Card, ToolModal
  },
  data () {
    return {
      results: [],
      isModalVisible: false,
    }
  },
   methods: {
      showModal() {
        this.isModalVisible = true;
      },
      closeModal() {
        this.isModalVisible = false;
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
