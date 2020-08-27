<template>
  <div class="app-container d-flex flex-column">

    <div class="bar-box my-4">
      <h4>Quotes Added</h4>
      <app-progress-bar :value="value"></app-progress-bar>
    </div>

    <main class="main-content d-flex flex-column">

      <div class="quote-input d-flex flex-column align-items-center w-100">
        <h4 class="quote-input__title">Quote</h4>
        <textarea name="quote-input__text" id="quote-input__text" class="w-50" v-model="quoteText" @keydown.enter.exact.prevent="sendText()"></textarea>
        <button class="btn btn-info my-3" @click="sendText()">Add Quote</button>
      </div>
      
      <div class="quote-list container">
        <div class="row justify-content-center">
          <app-quote 
          :message = "newMessage"
          v-for= "newMessage in messages" 
          :key="newMessage.id"
          @destroy-component = "destroyComponent = $event, elementDestroyed()"
          >
          </app-quote>
        </div>
      </div>
      
    </main>

    <footer class="main-footer">
      <app-footer></app-footer>
    </footer>
    
  </div>
</template>

<script>
  import Footer from './shared/Footer.vue';
  import Quote from './Quote.vue';
  import ProgressBar from './ProgressBar.vue'

  export default {
    components: {
      'app-footer' : Footer,
      'app-quote' : Quote,
      'app-progress-bar' : ProgressBar,
    },
    data() {
      return {
        quoteText : '',
        messages: [{
          id: 0,
          text: "We don't rise to the level of our expectations, we fall to the level of our training.",
        }],
        value: 10,
        destroyComponent: null,
      }
    },
    methods: {
      sendText() {
        if( this.quoteText != '' && this.value < 100){
          this.messages.push(
          {
            id: this.messages.length,
            text: this.quoteText
          }
        );
        this.value = this.messages.length * 10;
        this.quoteText = '';
        } else {
          if (this.value >= 100) {
            alert('You cannot add more quotes');
          } else{
            alert('Please insert some text to create a new quote');
          }
        }
      },
      elementDestroyed() {
        var index = this.messages.findIndex(x => x.id === this.destroyComponent);
        this.messages.splice(index, 1);
        this.value = this.messages.length * 10;
      }
    },
  }
</script>

<style scoped>

  .app-container{
    min-height: 100vh;
  }

  .bar-box{
    height: 20%;
  }

  .main-content{
    height: 75%;
    min-height: 70vh;
  }

  .main-footer{
    height: 5%;
  }

  textarea{
    outline: none;
    border: 1px solid #ccc;
    border-radius: 5px;
    transition: opacity 0.3s, background-color 0.6s;
  };
  textarea:active,
  textarea:focus{
    opacity: 1;
    background: rgb(228, 226, 226, 0.3);
  }
</style>