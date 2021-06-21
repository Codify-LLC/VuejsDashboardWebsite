<template>
    
      <div> 
        <Navbar v-on:clicked="onClickChild"/>
        <Sidebar v-on:changeSize="changeUploadContentPosition"/>
        
        <p class="uploadContentText" v-bind:style="{ left: computedLeft }">
          <strong>
            Upload Content
          </strong>
        </p>

        <UploadSection v-if="sectionShow" v-on:previewTrigger="sendImagePreviews" 
        :widthWrapper="widthWrapper" 
        :leftWrapper="leftWrapper"/>

        <UploadFormVideo 
        v-if="videoFormShow" 
        :files="files"
        :widthWrapper="widthWrapper" 
        :leftWrapper="leftWrapper" 
        v-on:uploadFile="sendFile">
        </UploadFormVideo>

        <UploadFormImg v-if="imgFormShow" :files="files" v-on:uploadFile="sendFile"
        :widthWrapper="widthWrapper" 
        :leftWrapper="leftWrapper"/>

        <UploadProgress v-if="progressShow" :files="files"
        :widthWrapper="widthWrapper" 
        :leftWrapper="leftWrapper"/>
      </div>
    
</template>

<script>
import Navbar from "./Navbar.vue"
import Sidebar from "./Sidebar.vue"
import UploadFormImg from "./UploadFormImg.vue"
import UploadFormVideo from "./UploadFormVideo.vue"
import UploadSection from "./UploadSection.vue"
import UploadProgress from "./UploadProgress.vue"
  export default {
    name: 'Dashboard',
    data() {
      return {
        instance: true, 
        imgFormShow: false, 
        videoFormShow: false, 
        sectionShow: true,
        progressShow: false,
        files: [],
        left: '14%',
        leftWrapper: '13%',
        widthWrapper: '80%'
        }
    },
    computed: {
      computedLeft: function () {
        return this.left;
      }
    },
    components: {
        Navbar,
        Sidebar,
        UploadFormImg,
        UploadFormVideo,
        UploadSection,
        UploadProgress,
    },
    methods: {
      onClickChild(value) {
        this.$emit('clicked', value)
      },

      changeUploadContentPosition() {
        if (this.left == "14%") {
          this.left = '25%'
          this.widthWrapper = '74%'
          this.leftWrapper = '24%'
        } else {
          this.left = '14%'
          this.leftWrapper = '13%'
          this.widthWrapper = '80%'
        }
      },

      sendImagePreviews(value){
        this.files = value;
        for( let i = 0; i < this.files.length; i++ ){
          if ( /\.(mp4)$/i.test( this.files[i].name ) ) {
            this.sectionShow = false
            this.videoFormShow = true
          } else  if ( /\.(jpe?g|png|gif)$/i.test( this.files[i].name ) ) {
            this.sectionShow = false
            this.imgFormShow = true
          }
        }
      },

      sendFile(){
        this.imgFormShow = false, 
        this.videoFormShow = false, 
        this.successShow = false, 
        this.sectionShow = false,
        this.progressShow = true
      },
    }
  }
  </script>

  <style>
    .uploadContentText{
        position: absolute;
        top: 20%;
        left: 14%;
        z-index: 200;
        transition: 0.5s;
    }
  </style>