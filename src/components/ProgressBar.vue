<template>
  <div class="bar-container">
    <div class="progress-bar bg-success" :style="{'width': value + '%'}">
      <span>{{ value }} %</span>
    </div>
  </div>

</template>

<script>
export default {
  props:{
    value: {
      type: Number,
      required: true,
    }
  }
}
</script>

<style>
  .bar-container{
    border: 1px solid #ccc;
    width: 1000px;
  };

</style>