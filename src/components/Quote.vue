<template>
  <div class="quote col-md-3 m-2" @click="deleteQuote()">
    <p class="quote__text p-3 text-center">
      "{{ message.text }}"
    </p>
  </div>
</template>

<script>
  export default {
    props:{
      message: {
        type: Object,
      }
    },
    methods:{
      deleteQuote() {
        console.log('Element id:', this.message.id, 'Destoyed');
        this.$emit('destroy-component', this.message.id);
        this.$destroy();
        this.$el.parentNode.removeChild(this.$el);
      }
    }
  }
</script>

<style scoped>
  .quote{
    border: 1px solid #ccc;
    border-radius: 5px;
    font-family: Arizonia;
    font-size: 28px;
    cursor: pointer;
    opacity: 0.8;
    transition: opacity 0.3s, background-color 0.6s;
    box-shadow: 3px 3px 3px rgba(0, 0, 0, 0.3);
  };
  .quote:hover{
    opacity: 1;
    background: rgb(228, 226, 226, 0.3);
  }
</style>