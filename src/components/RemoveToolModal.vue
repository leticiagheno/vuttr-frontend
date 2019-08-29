<template>
  <div v-if="showModal">
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title"> Remove Tool </h5>
                </div>
                <div class="modal-body">
                    <form>
                      <div>
                      <label> Are you sure you want to remove {{ tool.title }} ?</label>
                      </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" @click="resetModal()" class="btn btn-primary">Cancel</button>
                    <button type="button" @click="resetModal()" class="btn btn-primary">Yes, remove tool</button>
                </div>
            </div>
        </div>
        </div>
      </div>
    </transition>
  </div>
</template>

<script>
import axios from 'axios';
import {EventBus} from '../main.js'

export default {
  name: "remove-tool-modal",
  props: ['showModal', 'tool'],
  methods: {
    resetModal() {
        axios
        .delete('http://localhost:3000/tools/' + this.tool._id);
        this.$emit('update:showModal', false);
        EventBus.$emit('deleteTool', this.tool);
    }
  }
};

</script>

<style scoped>

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
