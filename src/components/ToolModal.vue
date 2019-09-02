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
                    <input 
                      class="col-sm-12 input-area form-control" 
                      v-model="title" 
                      type="text" 
                      required
                    /> 
                    <label> Tool Link </label>
                    <input 
                      class="col-sm-12 input-area form-control" 
                      v-model="link" 
                      type="text" 
                      required 
                    />
                    <label> Tool Description </label>
                    <textarea 
                      class="col-sm-12 text-area form-control" 
                      v-model="description"
                    />
                    <div class="row col-sm-12">
                      <label> Tags </label>
                      <img class="help-image" v-bind:title="tagMessage" src="../assets/Icon-Learn-2px.png"/>
                    </div>
                    <input-tag
                      v-model="tagsAdd"
                      class="col-sm-12 form-control input-area"
                    />
                    <div class="row justify-content-end">
                      <input 
                        class="col-sm-6 col-md-4 button-primary-neutral" 
                        type="submit" 
                        value="Add tool"
                      />
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
import axios from "axios";
import InputTag from "vue-input-tag";

export default {
  name: "tool-modal",
  props: ["showModal"],
  components: {
    InputTag
  },
  data() {
    return {
      title: "",
      link: "",
      description: "", 
      tags: "", 
      tagsAdd: [],
      tagMessage: "Para adicionar uma tag, basta escrever e após, dar enter."
    };
  },
  methods: {
    saveTool() {
      var config = {
        headers: {"x-access-token": localStorage.getItem("access-token") }
      }; 
      axios.post("http://localhost:3000/tools", { 
        title: this.title, 
        link: this.link, 
        description: this.description,
        tags: this.tagsAdd
      }, 
      config)
      .then((response) => {
        this.$emit("newTool", response);
        Object.assign(this.$data, this.$options.data());
      });
      this.$emit("update:showModal", false);
    },
    closeModal() {
      this.$emit("update:showModal", false);
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

.help-image {
  background: transparent 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 17px;
  width: 17px;
  margin-left: 7px;
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
  background: #f5f4f6 0% 0% no-repeat padding-box;
  border: 1px solid #ebeaed;
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}

.input-area:focus {
  background: #ebeaed 0% 0% no-repeat padding-box;
  border: 1px solid #dedce1;
  border-radius: 5px;
  opacity: 1;
  padding: 0px 5px;
}

.input-area {
  background: #ebeaed 0% 0% no-repeat padding-box;
  border: 1px solid #dedce1;
  border-radius: 5px;
  opacity: 1;
  padding: 5px 5px;
}

.text-area {
  margin-bottom: 10px;
  background: #f5f4f6 0% 0% no-repeat padding-box;
  border: 1px solid #ebeaed;
  border-radius: 5px;
  opacity: 1;
  padding: 5px 5px;
}

.text-area:focus {
  background: #ebeaed 0% 0% no-repeat padding-box;
  border: 1px solid #dedce1;
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
  background: #365df0 0% 0% no-repeat padding-box;
  color: white;
  border: transparent;
  border-radius: 5px;
  opacity: 1;
  margin: 0px 15px;
}

.button-primary-neutral:hover {
  background: #2f55cc 0% 0% no-repeat padding-box;
}

.button-primary-neutral:focus {
  background: #365df0 0% 0% no-repeat padding-box;
}
</style>
