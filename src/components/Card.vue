<template>
  <div class="home">
    <div id="card" >
    <a id="name-item" v-bind:href='tool.link'> {{ tool.title }} </a>
    <p class="text-card"> {{ tool.description }} </p>
    <div class="row" > 
    <p v-for="tag in tool.tags" :key="tag.id" class="text-card"> # {{ tag }} </p> 
    </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "card-item",
  props: ['tool']
};
</script>

<style>

#card {
    width: 750px;
    height: 200px;
    background: #FFFFFF 0% 0% no-repeat padding-box;
    box-shadow: 0px 5px 7px #000000;
    border: 1px solid #EBEAED;
    border-radius: 5px;
    opacity: 1;
}

#name-item {
  text-align: left;
}

.text-card {
  text-align: left;
  font: Regular 20px/26px Source Sans Pro;
  letter-spacing: 0.4px;
  color: #170C3A;
  opacity: 1;
}

</style>
