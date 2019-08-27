<template>
  <div v-if="showModal">
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title"> Add new tool </h5>
                </div>
                <div class="modal-body">
                    <form>
                      <div>
                      <label> Tool Name </label>
                      <input class="col-12 input-area" v-model="title" type="text"/> 
                      <label> Tool Link </label>
                      <input class="col-12 input-area" v-model="link" type="text"/>
                      <label> Tool Description </label>
                      <textarea class="col-12 input-area" v-model="description"/>
                      <label> Tags </label>
                      <input class="col-12 input-area" v-model="tags" type="text"/>
                      </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" @click="saveTool()" class="btn btn-primary">Add tool</button>
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

export default {
  name: "tool-modal",
  props: ['showModal'],
  data() {
    return {
      title: '',
      link: '',
      description: '', 
      tags: ''
    }
  },
  methods: {
    saveTool() {
      axios.post('http://localhost:3000/tools', { title: this.title, 
        link: this.link, 
        description: this.description,
        tags: this.tags.split(" ") 
      })
      .then((response) => {
        this.$emit('newTool', response);
        Object.assign(this.$data, this.$options.data());
      });  
      this.$emit('update:showModal', false);
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