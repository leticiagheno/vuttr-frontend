<template>
  <div class="home align-items-center">
    <div class="col-12 justify-content-center display-flex" > 
    <h1 id="page-title"> VUTTR </h1> 
    <h3 id="page-subtitle"> Very Useful Tools To Remember </h3> 
    <div class="row col-12 justify-content-between display-flex ">
    <div class="row col-8 align-items-center" id="items-bar">
    <input id="search-item" type="search" class="col-6" placeholder="Search..."/>
    <input id="tags-check" class="col-1" type="checkbox"/> Search in tags only
    </div>
    <div class="col-2">
      <button class="col-12 align-self-end" @click="openModal()" > Add </button>
    </div>
    </div>
    </div>
      <transition-group name="list-tools" tag="div">
        <Card v-for="tool in results" v-bind:key="tool._id" :tool="tool" class="list-items" />
     </transition-group>
    <ToolModal
        :showModal.sync="showModal"
        v-on:newTool="newTool"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Card from "@/components/Card.vue";
import ToolModal from '@/components/ToolModal.vue';
import axios from 'axios';
import {EventBus} from '../main.js';

export default {

  name: "home-page",
  components: {
    Card, ToolModal
  },
  data () {
    return {
      results: [],
      showModal: false
    }
  },
  created(){
        EventBus.$on('deleteTool', (tool) => {
            var index = this.results.indexOf(tool);
            this.results.splice(index, 1);
        });
    },
   methods: {
      openModal() {
        this.showModal = true;
      }, 
      newTool(response) {
        this.showModal = false;
        this.results.push(response.data.result);
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

.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-tools-enter-active, .list-tools-leave-active {
  transition: all 1s;
}
.list-tools-enter, .list-tools-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-tools-move {
  transition: transform 1s;
}

</style>
