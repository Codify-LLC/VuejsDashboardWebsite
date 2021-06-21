<template>
  <div class="bgsignIn">
    <div class="form">
      <div class="logo_signIn">
        <img alt="Flyer Logo" class="logo" src="../../assets/FLYERLOGO.png" />
        <div class="btn_inp">
          <div class="btnSelect">
            <div class="btn-group" role="group" aria-label="Basic example">
              <button type="button" class="numBtn btn btn-primary" :class="instance ? '' : 'btnBg'" @click="toggle">Number</button>
              <button type="button" class="emailBtn btn btn-primary" :class="!instance ? '' : 'btnBg'" @click="toggle">Email</button>
            </div>
          </div>
        <div class="box" style="background: #6789C3"></div>
        <transition name="fade" :class="instance ? '' : 'btnBg'">
          <numberfield v-on:clicked="onClickChild" v-if="!instance" class="zNum"></numberfield>
        </transition>
        <transition name="fade" :class="!instance ? '' : 'btnBg'">
          <emailfield v-on:clicked="onClickChild" v-if="instance" class="zEmail"></emailfield>
        </transition>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import numberfield from './Numberfield.vue';
import emailfield from './Emailfield.vue';
  export default {
    name: 'SignIn',
    data() {
      return {instance: true}
      
    },
    components: {
      numberfield,
      emailfield
    },
    methods: {
      toggle() {
        // `this` will refer to the component instance
        if (this.instance) {
          this.instance = false
        } else {
          this.instance = true
        }
      },
      onClickChild(value) {
        this.$emit('clicked', value)
      }
    }
  }
  </script>
  <style scoped>
    .bgsignIn{
      min-height: 100vh !important;
      min-width: 100vw  !important;
      background-color: #3865B0;
      display: flex;
      justify-content: center;
      align-items: center;
    }
    .form {
      background: #789AD4;
      display: flex;
      justify-content: center;
      align-items: center;
      width: 405px;
      height: 438px;
      margin: auto;
      border-radius: 15px;
    }
    .logo {
      max-height: 100px;
      max-width: 100px;
    }
    .btn_inp {
      margin-top: 40px;
      height: 193px;
      justify-content: center;
      align-items: center;
    }
    .numBtn {
      width: calc(324px/2);
      height: 48px;
      background: #789AD4;
      border: 1px solid #3865B0;
      border-radius: 10px 0px 0px 0px;
    }
    .emailBtn {
      width: calc(324px/2);
      height: 48px;
      border: 1px solid #3865B0;
      background: #789AD4;
      border-radius: 0px 10px 0px 0px;
    }
    .btnBg{
      background: #3865B0 !important;
      transition: 0.6s ease;
    }
    .box {
      display: flex;
      justify-content: center;
      align-items: center;
      width: 324px;
      height: 145px;
      background: #3865B0;
      z-index: 1;
      border-radius: 0px 0px 10px 10px;
      position: absolute;
    }
    input {
      width: 253px !important;
      height: 34px;
      background-color: white;
      border-radius: 20px !important;
      border: none;
      outline: none;
    }
    .signIn {
      width: 253px;
      height: 34px;
      border-radius: 20px !important;
      background: transparent !important;
      border: 1px solid #fff !important;
    }
  </style>