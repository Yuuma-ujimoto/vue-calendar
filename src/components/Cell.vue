<template>
  <div class="Cell" :class="{'isBlank':type==='blank','date':type==='default'}">
    {{date}}
  </div>

</template>

<script>
export default {
  name: "Cell",
  props:{
    type:String,
    date:String
  }
}
</script>

<style scoped>
  .Cell{
    width: 110px;
    height: 110px;
    border: solid 1px black;
    box-sizing: border-box;
    margin: 5px;
    padding: 10px;
  }
  .isBlank{
    background: gray;
    color: white;
  }
  .date{
    height: 50px;
    background: azure;
  }
</style>