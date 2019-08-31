<template>
  <div v-if="showModal">
    <transition name="modal">
      <div class="modal-mask">
        <div class="modal-wrapper">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header align-center justify-content-between align-self-center col-12">
                  <div class="row col-8 align-center">
                    <img class="add-image" src="../assets/Icon-Close-2px.png"/>
                    <h5 class="modal-title align-start"> Add new tool </h5>
                  </div>
                  <div class="col-1">
                    <img class="close-image" @click="closeModal" src="../assets/Icon-Close-2px.png"/>
                  </div>
                </div>
                <div class="modal-body">
                    <form @submit="saveTool">
                      <div>
                      <label> Tool Name </label>
                      <input class="col-sm-12 input-area" v-model="title" type="text" required oninvalid="You must fill out the form!"/> 
                      <label> Tool Link </label>
                      <input class="col-sm-12 input-area" v-model="link" type="text" required />
                      <label> Tool Description </label>
                      <textarea class="col-sm-12 text-area" v-model="description"/>
                      <label> Tags </label>
                      <input class="col-sm-12 input-area" v-model="tags" type="text"/>
                      <div class="row justify-content-end">
                        <input class="col-sm-6 col-md-4 button-primary-neutral" type="submit" value="Add tool">
                      </div>
                      </div> 
                    </form>
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
    }, 
    closeModal() {
      this.$emit('update:showModal', false);
    }
  }
};

</script>

<style scoped>

.align-center {
  align-items: center;
}

.close-image {
  background: transparent 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 15px;
  width: 15px;
}

.add-image {
  background: transparent 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 15px;
  width: 15px;
  margin-right: 15px;
  transform: rotate(45deg);
}

.input-area {
  margin-bottom: 10px;
  background: #F5F4F6 0% 0% no-repeat padding-box;
  border: 1px solid #EBEAED;  
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}

.input-area:focus {
  background: #EBEAED 0% 0% no-repeat padding-box;
  border: 1px solid #DEDCE1;
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}

.input-area {
  background: #EBEAED 0% 0% no-repeat padding-box;
  border: 1px solid #DEDCE1;
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}


.text-area {
  margin-bottom: 10px;
  background: #F5F4F6 0% 0% no-repeat padding-box;
  border: 1px solid #EBEAED;
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}

.text-area:focus {
  background: #EBEAED 0% 0% no-repeat padding-box;
  border: 1px solid #DEDCE1;
  border-radius: 5px;
  opacity: 1;
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

.button-primary-neutral {
  background: #365DF0 0% 0% no-repeat padding-box;
  color: white;
  border-radius: 5px;
  opacity: 1;
  margin: 0px 15px;
}

.button-primary-neutral:hover {
  background: #2F55CC 0% 0% no-repeat padding-box;
  color: white;
  border-radius: 5px;
  opacity: 1;
  margin: 0px 15px;
}

.button-primary-neutral:focus {
  background: #365DF0 0% 0% no-repeat padding-box;
  color: white;
  border-radius: 5px;
  opacity: 1;
  margin: 0px 15px;
}

</style>