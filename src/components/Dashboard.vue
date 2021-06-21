<template>
    
      <div> 
        <Navbar v-on:clicked="onClickChild"/>
        <Sidebar/>
        <p class="uploadContentText">
          <strong>
            Upload Content
          </strong>
        </p>
        <UploadSection v-if="sectionShow" v-on:previewTrigger="sendImagePreviews"/>
        <UploadFormVideo v-if="videoFormShow" :files="files" v-on:uploadFile="sendFile"/>
        <UploadFormImg v-if="imgFormShow" :files="files" v-on:uploadFile="sendFile"/>
        <UploadProgress v-if="progressShow" :files="files"/>
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
      left: 22%;
      z-index: 200;
    }
  </style>