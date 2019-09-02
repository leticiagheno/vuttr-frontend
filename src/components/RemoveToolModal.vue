<template>
  <div v-if="showModal">
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
          <div class="modal-dialog" role="document">
            <div class="modal-content">
              <div class="modal-header">
                <div class="row align-items-center col-12">
                  <img 
                    class="remove-image" 
                    src="../assets/Icon-Close-2px.png"/>
                  <h5 
                    class="align-start align-self-start remove-title"
                  > Remove Tool </h5>
                </div>  
              </div>
              <div class="modal-body">
                <div>
                  <label> Are you sure you want to remove {{ tool.title }} ?</label>
                </div>
              </div>
              <div class="modal-footer">
                <button 
                  type="button" 
                  @click="cancelModal()" 
                  class="cancel-button"
                > Cancel </button>
                <button 
                  type="button" 
                  @click="removeTool()" 
                  class="remove-button"
                > Yes, remove tool </button>
              </div>
            </div>
          </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import axios from "axios";
import {EventBus} from "../main.js"

export default {
  name: "remove-tool-modal",
  props: [
    "showModal", 
    "tool"
  ],
  methods: {
    removeTool() {
      var config = {
        headers: { "x-access-token": localStorage.getItem("access-token") }
      };
      axios
        .delete("http://localhost:3000/tools/" + this.tool._id, config);
      this.$emit("update:showModal", false);
      EventBus.$emit("deleteTool", this.tool);
    },
    cancelModal(){
      this.$emit("update:showModal", false);
    }
  }
};

</script>

<style scoped>

.remove-image {
  background: transparent url("../assets/Icon-Close-2px.png") 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 15px;
  width: 15px;
}

.remove-button {
  background: #f95e5a 0% 0% no-repeat padding-box;
  border: none;
  border-radius: 5px;
  opacity: 1;
  text-align: center;
  font: Semibold 18px/24px Source Sans Pro;
  letter-spacing: 0.36px;
  color: #FFFFFF;
}

.remove-button:hover {
  background: #cc4c4c 0% 0% no-repeat padding-box;  
}

.remove-button:active {
  background: #a53f3f 0% 0% no-repeat padding-box;
}

.cancel-button {
  background: #e1e7fd 0% 0% no-repeat padding-box;
  border: none;
  border-radius: 5px;
  opacity: 1;
  text-align: center;
  font: Semibold 18px/24px Source Sans Pro;
  letter-spacing: 0.36px;
  color: #365fd0;
}

.cancel-button:hover {
  background: #cad6fc 0% 0% no-repeat padding-box;  
}

.cancel-button:active {
  background: #b9c6fa 0% 0% no-repeat padding-box;
}

.remove-title {
  text-align: left;
  font: Semibold 24px/30px Source Sans Pro;
  letter-spacing: 0.48px;
  color: #170c3a;
  opacity: 1;
  margin: 10px;
}

.input-area {
  margin-bottom: 10px;
}

.modal-body {
  text-align: left;
  display: block;
  letter-spacing: 0.6px;
  opacity: 1;
}

.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, .5);
  display: table;
  transition: opacity .3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

</style>
