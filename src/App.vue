<template>
  <div id="app">

    <signIn v-on:clicked="onClickChild" v-if="pageToggle"/>
    <dashboard v-on:clicked="onClickChild" v-if="!pageToggle"/>

  </div>
</template>

<script>
  import Vue from 'vue'
  Vue.$showToggle = true
  import signIn from "./components/SignIn.vue";
  import dashboard from "./components/Dashboard.vue"
  export default {
    name: "App",
    data() {
      return{pageToggle: true}
    },
    components: {
      signIn,
      dashboard
    },
    methods: {
      onClickChild (value) {
        this.pageToggle = value
        console.log(value) // someValue
      }
    }
  };
  </script>

  <style>
    #app {
      font-family: 'Rubik', sans-serif;
      text-align: center;
    }

    #app img {
      height: 200px;
      width: 200px;
    }

    .zNum {
      z-index: 80;
    }

    .zEmail {
      z-index: 0;
    }

    .fade-enter-active{
        transition: opacity 0.6s;
    }
    .fade-leave-active {
        opacity: 0;
    }
    .fade-enter, .fade-leave-to {
        opacity: 0;
    }
  </style>