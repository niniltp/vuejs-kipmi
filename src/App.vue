<template>
  <div id="app">
    <notifications group="general"
                   position="top right"
                   :speed="700" :duration="6000" :width="400" class="notification-title notification-content"/>
    <h1>Kipmi</h1>
    <Quotes v-on:show="show"></Quotes>
  </div>
</template>

<script>
import Quotes from './components/Quotes.vue'

export default {
  name: 'app',
  components: {
    Quotes
  },
  methods: {
    show (notif) {
      this.$notify(notif)
    },
    clean (group) {
      this.$notify({ group, clean: true })
    }
  }
}
</script>

<style>
  @import url('https://fonts.googleapis.com/css?family=Montserrat:400,700');
  @import "https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css";
  @import "https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css";                                                                                                                                                                                                                                                                                                                                              <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/js/bootstrap.min.js" integrity="sha384-JZR6Spejh4U02d8jOt6vLEHfe/JQGiRRSQQxSfFWpi1MquVdAyjUar5+76PVCmYl" crossorigin="anonymous"></script>

  body {
    background-color: #EEEEEE;
    font-family: 'Montserrat', sans-serif;
    font-size: 1.3em;
    display: grid;
    grid-template-rows: auto;
    justify-items: center;
    align-items: center;
  }
  body, html {
    margin: 0;
    height: 100%;
  }

  h1 {
    text-align: center;
    font-size: 4em;
    margin: 30px;
  }

  a {
    color: #3EB3F6;
  }

  a:hover {
    color: #3E5252;
    text-decoration: underline;
  }

  input, textarea {
    width: 100%;
    border: 0;
    padding: 20px;
    font-size: 1.3em;
    background-color: #323333;
    color: #a0adb7;
  }

  textarea {
    resize: vertical;
    overflow: auto;
  }

  input:focus, textarea:focus {
    background-color: #373838;
    outline: none;
  }


  .notification-title {
    font-size: 2em;
  }

  .notification-content {
    font-size: 1.5em;
  }
</style>
