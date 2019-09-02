<template>
  <div class="home align-items-center">
    <div class="col-12 justify-content-center display-flex superior-div" > 
      <div class="row col-12 justify-content-between">
        <h1 id="page-title"> VUTTR </h1> 
        <button 
          @click="logout" class="logout-button"
        > Logout </button>
      </div>
      <h3 id="page-subtitle"> Very Useful Tools To Remember </h3> 
      <div class="row col-12 justify-content-between display-flex items-bar">
        <div class="row col-12 col-sm-12 col-md-10 align-items-center">        
          <input 
            id="search-item" 
            type="search" 
            @input="searchTool" 
            v-model="textSearch" 
            class="col-sm-12 col-md-6" 
            placeholder="Search..."
          >
          <input 
            id="tags-check" 
            class="col-sm-2 col-md-1" 
            v-model="checked" 
            type="checkbox"
          /> Search in tags only 
        </div>
        <div class="col-sm-12 col-md-2">
          <button 
            class="col-sm-12 align-self-end add-button" 
            @click="openModal()"
          > 
            <img 
              class="add-image" 
              src="../assets/Icon-Close-2px.png"
            /> Add 
          </button>
        </div>
      </div>
    </div>
    <transition-group 
      name="list-tools" 
      tag="div">
      <Card 
        v-for="tool in results" 
        v-bind:key="tool._id" 
        :tool="tool" 
        class="list-items" 
      />
    </transition-group>
    <ToolModal
      :showModal.sync="showModal" v-on:newTool="newTool"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import Card from "@/components/Card.vue";
import ToolModal from "@/components/ToolModal.vue";
import axios from "axios";
import {EventBus} from "../main.js";
import * as jwt from "jsonwebtoken";
import router from "../router";

export default {
  name: "home-page",
  components: {
    Card, 
    ToolModal
  },
  data() {
    return {
      results: [],
      checked: false,
      textSearch: "",
      showModal: false
    };
  },
  created() {
    EventBus.$on("deleteTool", (tool) => {
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
    },
    searchTool() {
      var config = {
        headers: { "x-access-token": localStorage.getItem("access-token") }
      };

      var vm = this;
      if (this.textSearch === "") {
        axios
          .get("http://localhost:3000/tools", config)
          .then(response => {
            vm.results = response.data.result;
          });
      } else if (this.checked) {
        axios
          .get("http://localhost:3000/tools?tag=" + this.textSearch, config)
          .then(response => {
            vm.results = response.data.result;
          });
      } else {
        axios
          .get("http://localhost:3000/tools?global=" + this.textSearch, config)
          .then(response => {
            vm.results = response.data.result;
          });
      }
    },
    logout() {
      localStorage.setItem("access-token", null);
      router.push({ name: "signin" });
    }
  },
  beforeMount() {
    var config = {
      headers: { "x-access-token": localStorage.getItem("access-token") }
    };
    var accessToken = localStorage.getItem("access-token");
    var vm = this;

    jwt.verify(accessToken, "desafio bossaBox", function(err) {
      if (err) {
        router.push({ name: "signin" });
      } else {
        axios
          .get("http://localhost:3000/tools", config)
          .then(response => {vm.results = response.data.result})
      }
    });
  }
};
</script>

<style scoped>
.logout-button {
  text-align: end;
  font: Semibold 18px/24px Source Sans Pro;
  letter-spacing: 0.36px;
  color: #365df0;
  border: none;
  opacity: 1;
  background: transparent;
  border-radius: 5px;
  margin-top: 10px;
  opacity: 1;
  width: 120px;
  height: 35px;
}

.add-button {
  background: #e1e7fd 0% 0% no-repeat padding-box;
  border: transparent;
  border-radius: 5px;
  color: #365df0;
  font: Semibold 18px/24px Source Sans Pro;
  opacity: 1;
  letter-spacing: 0.36px;
  text-align: center;
  width: 174px;
  height: 35px;
}

.add-button:hover {
  background: #cad6fc 0% 0% no-repeat padding-box;
}

.add-button:active {
  background: #b9c6fa 0% 0% no-repeat padding-box;
}

.items-bar {
  padding-right: 0px;
}

.superior-div {
  padding-right: 0px;
}

.add-image {
  background: transparent 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 10px;
  width: 10px;
  margin-right: 15px;
  transform: rotate(45deg);
}

#page-title {
  text-align: left;
  font: Semibold 42px/50px Source Sans Pro;
  letter-spacing: 0.84px;
  color: #170c3a;
  opacity: 1;
}

#page-subtitle {
  text-align: left;
  font: Semibold 36px/40px Source Sans Pro;
  letter-spacing: 0.72px;
  color: #170c3a;
  opacity: 1;
}

#search-item {
  background: #f5f4f6 0% 0% no-repeat padding-box;
  border: 1px solid #ebeaed;
  border-radius: 5px;
  opacity: 1;
  width: 403px;
  height: 50px;
}

.list-item {
  display: inline-block;
  margin-right: 10px;
}

.list-tools-enter-active, 
.list-tools-leave-active {
  transition: all 1s;
}

.list-tools-enter, 
.list-tools-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.list-tools-move {
  transition: transform 1s;
}
</style>
