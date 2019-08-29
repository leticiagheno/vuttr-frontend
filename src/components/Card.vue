<template>
  <div class="home">
    <div id="card">
      <div class="row justify-content-between">
        <h3 class="col-md-6 col-sm-4" > <a id="name-item" v-bind:href='tool.link'> {{ tool.title }} </a></h3>
        <a class="col-md-2 col-sm-2" @click="openRemoveToolModal()"> <img class="remove-image" src="../assets/Icon-Close-2px.png"/> remove </a>
        </div>
    <p class="text-card"> {{ tool.description }} </p>
    <div class="row tag-div"> 
    <b v-for="tag in tool.tags" :key="tag.id" class="text-card"> #{{ tag }} &nbsp; </b> 
    </div>
    <RemoveToolModal
        :showModal.sync="showModal"
        :tool="tool"
        :key="tool._id"
    />
    </div>
  </div>
</template>

<script>
import RemoveToolModal from '@/components/RemoveToolModal.vue';

export default {
  name: "card-item",
  components: {
    RemoveToolModal
  },
  props: ['tool'],
  data () {
    return {
      showModal: false
    }
  },
   methods: {
      openRemoveToolModal() {
        this.showModal = true;
      },
      resetModal() {
        this.showModal = false;
      }
    },
};
</script>

<style>

#card {
    background: #FFFFFF 0% 0% no-repeat padding-box;
    border: 1px solid #EBEAED;
    border-radius: 5px;
    opacity: 1;
    padding: 20px;
    margin: 10px;
}

#name-item {
  text-align: left;
  display: block;
  letter-spacing: 0.6px;
  opacity: 1;
}

.remove-image {
  background: transparent url('../assets/Icon-Close-2px.png') 0% 0% no-repeat padding-box;
  opacity: 1;
  height: 15px;
  width: 15px;
}

.text-card {
  text-align: left;
  font: Regular 20px/26px Source Sans Pro;
  letter-spacing: 0.4px;
  color: #170C3A;
  opacity: 1;
}

.tag-div {
  padding-left: 15px;
}

</style>
