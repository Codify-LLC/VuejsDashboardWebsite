<template>
    <!-- SIDEBAR -->
    <div class="sidebar_navigation">
    <input type="checkbox" id="btnControl"/>
      <label class="btn" for="btnControl">
        <div class="sidebar_navigation">
            <div class="spaceAbove">
            <div>
                <img class="dashboardUser" src="../../assets/img.jpeg" alt="" />
            </div>
            <div class="Sidebar_userName">
                USER : FULL NAME
            </div>
            </div>
            <ul>
            <li>
                <a href="#">
                <span class="icon"><img class="contentIcon" src="../../assets/contentIcon.png"/></span>
                <span class="title">Dashboard</span>
                </a>
            </li>
            </ul>
        </div>
      </label>
    </div>
    <!-- SIDEBAR END -->
</template>

<script>
  export default {
    name: 'Sidebar',
    props: {
      msg: String
    }
  }
  </script>

<style>
     /* SIDEBAR */
    .sidebar_navigation {
      position: fixed;
      top: 0px;
      left: 0;
      width: 75px;
      height: 100%;
      background-color: white;
      transition: 0.5s;
      overflow: hidden;
      z-index: 100;
    }
    #btnControl:checked + label > .sidebar_navigation {
      width: 250px;
      transition: 0.5s;
    }
    #btnControl:checked + label > .sidebar_navigation .dashboardUser {
      
      height: 100px !important;
      width: 100px !important;
      transition: 0.8s;
    }
    #btnControl:checked + label > .sidebar_navigation .Sidebar_userName {
      display: block;
      animation: fadein 1s;
      transition: 2s;
    }

    @keyframes fadein {
      from { opacity: 0; }
      to   { opacity: 1; }
    }
    
    .sidebar_navigation ul {
      position: relative;
      top: 0;
      left: 0;
      width: 100%;
      background-color: #EEEEEE;
      height: 60px;
      border-left: 4px solid #3865B0;
    }
    .dashboardUser {
      height: 55px !important;
      width: 55px !important;
      border-radius: 50%;
      margin: auto !important;
      margin-top: 2rem;
    }
    .Sidebar_userName {
      margin: 1.3rem 0;
      color: black;
      display: none;
      font-weight: 400;
      transition: 2s;
    }
    .sidebar_navigation ul li {
      margin-top: 2rem;
      position: relative;
      width: 100%;
      list-style: none;
    }
    .sidebar_navigation ul li a {
      position: relative;
      display: block;
      width: 100%;
      display: flex;
      text-decoration: none;
      color: #3865B0;
      
    }
    .sidebar_navigation ul li a .icon {
      position: relative;
      display: flex;
      align-items: center;
    }
    .contentIcon{
      height: 23px !important;
      width: 23px !important;
      margin: 18px 0px;
      margin-left: -7px;
    }
    .sidebar_navigation ul li a .title {
      position: relative;
      display: block;
      padding: 0 25px;
      height: 60px;
      line-height: 60px;
      text-align: start;
      font-size: 18px;
      font-weight: 400;
    }
    .spaceAbove {
      margin-top: 100px;
    }
</style>