<template>
  <div class="box">
    <form>
      <div class="row mb-3">
        <div class="col-sm-10">
          <input type="number" class="form-control" id="inpNumber" placeholder="Number">
        </div>
      </div>
      <button type="button" class="signIn btn btn-primary" @click="onClickButton()">Sign In</button>
    </form>
  </div>
</template>

<script>
  import Vue from 'vue'
  export default {
    name: 'Numberfield',
    methods: {
      onClickButton () {
        console.log(Vue.$showToggle),
        this.$emit('clicked', false)
      }
    }
  }

  </script>
  <style scoped>
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
      background: #3865B0;
      border-radius: 0px 10px 0px 0px;
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