<template>
<!-- HEADER -->
  <div>
    <div class="bgdashboard"></div>
    <nav class="navbar navbar-expand-lg">
      <div class="container-fluid">
        <div class="d-flex justify-content-center" id="">
          <ul class="navbar-nav me-auto my-2 my-lg-0 navbar-nav-scroll" style="--bs-scroll-height: 100px;">
            <li class="nav-item">
              <label class="btn" for="btnControl"><i class="nav_bar fas fa-bars"></i></label>
            </li>
            <li class="nav-item">
              <img class="navbar_flyer_logo" src="../../assets/FLYERLOGO.png" alt="" />
            </li>
          </ul>
          <input type="checkbox" id="btnControl2"/>
          <label class="btn" for="btnControl2">
            <div class="d-flex">
                <img class="userLogo" src="../../assets/img.jpeg" alt="" />
            </div>
          </label>
          <label class="btn" for="btnControl2" @click="onClickButton()">
            <div class="logoutSection">
                <svg class="logoutsvg" width="23" height="23" viewBox="0 0 25 25" fill="none" xmlns="http://www.w3.org/2000/svg">
                <g clip-path="url(#clip0)">
                    <path d="M12.4585 22.8821H3.1146C2.5415 22.8821 2.07642 22.4169 2.07642 21.8439V3.15615C2.07642 2.58306 2.54155 2.11797 3.1146 2.11797H12.4585C13.0326 2.11797 13.4967 1.65391 13.4967 1.07979C13.4967 0.505664 13.0326 0.0415039 12.4585 0.0415039H3.1146C1.39741 0.0415039 0 1.43896 0 3.15615V21.8438C0 23.561 1.39741 24.9584 3.1146 24.9584H12.4585C13.0326 24.9584 13.4967 24.4944 13.4967 23.9203C13.4967 23.3461 13.0326 22.8821 12.4585 22.8821Z" fill="#646464"/>
                    <path d="M24.6906 11.7608L18.3783 5.53156C17.9713 5.12873 17.3131 5.13395 16.9103 5.54196C16.5075 5.94997 16.5116 6.60714 16.9207 7.00998L21.4317 11.4618H9.34385C8.76973 11.4618 8.30566 11.9258 8.30566 12.5C8.30566 13.0741 8.76973 13.5382 9.34385 13.5382H21.4317L16.9207 17.99C16.5117 18.3928 16.5085 19.05 16.9103 19.458C17.1138 19.6636 17.3816 19.7674 17.6495 19.7674C17.9132 19.7674 18.1769 19.6677 18.3783 19.4684L24.6906 13.2391C24.8879 13.044 25 12.7781 25 12.4999C25 12.2218 24.8889 11.957 24.6906 11.7608Z" fill="#646464"/>
                </g>
                    <defs>
                    <clipPath id="clip0">
                        <rect width="25" height="25" fill="white"/>
                    </clipPath>
                    </defs>
                </svg>
                <p class="logoutText">Log Out</p>
            </div>
          </label>
        </div>
      </div>
    </nav>
  </div>
  <!-- HEADER END -->
</template>

<script>
    import Vue from 'vue'
    export default {
        name: 'Navbar',
        methods: {
            onClickButton () {
                console.log(Vue.$showToggle),
                this.$emit('clicked', true)
            }
        }
    }
  </script>

<style>
    .navbar-nav{
        flex-direction: row !important;
    }
    #btnControl, #btnControl2 {
      margin-top: 10px;
      display: none;
    }

    #btnControl:checked + label > div {
        width: 250px;
        
    }

    /* NAVBAR */
    .bgdashboard{
      min-height: 100vh;
      min-width: 100vw;
      background-color: #eee;
      z-index: -200;
    }
    nav {
      height: 70px !important;
      position: fixed !important;
      top: 0;
      left: 0;
      background-color: #3865B0;
      width: 100vw !important;
      display: flex;
      justify-content: left;
      z-index: 200;
    }
    .nav_bar {
      margin: 27px 32px;
      font-size: 24px;
      color: white;
    }
    .navbar_flyer_logo {
      margin: 20px 40px;
      height: 55px !important;
      width: 55px !important;
    }
    .userLogo {
      height: 55px !important;
      width: 55px !important;
      border-radius: 50%;
      float: left;
      position: fixed;
      right: 30px;
      top: 8px;
    }
    #btnControl2:checked + label + label > .logoutSection {
      display: flex;
    }
    .logoutSection{
      position: absolute;
      width: 219px;
      height: 64px;
      right: 30px;
      top: 68px;
      background: #FFFFFF;
      box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.25);
      display: flex;
      flex-direction: row;
      justify-content: left;
      align-items: center;
      display: none;
    }
    .logoutsvg{
      margin-left: 20px;
    }
    .logoutText{
      margin: 10px 22px;
      font-size: 12px;
    }
</style>