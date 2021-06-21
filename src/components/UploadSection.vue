<style>
.inp_label{
  width: 300px;
  margin: auto;
  margin-top: 100px;
}
.inp_holder{
  width: 200px;
  margin: auto;
}
.dropzone {
    padding: 0.5rem;
}
.btn_upload{
  background-color: #3865B0;
  width: 100px;
  height: 35px;
  display: inline-grid;
}
.dropzone-wrapper {
    position: absolute;
    width: 837px;
    height: 393px;
    left: 277px;
    top: 147px;
    background: #FFFFFF;
}
.btn_upload::-webkit-file-upload-button {
  background-color: #3865B0;
  visibility: hidden;
}
.btn_upload::before {
  border-color: transparent;
  background-color: transparent;
  content: 'Select file';  padding: 0;
  outline: none;
  white-space: nowrap;
  cursor: pointer;
  text-shadow: 0.5px 0.5px #000;
  font-weight: 700;
  font-size: 10pt;
  text-align: center;
  color: white;
}
.btn_upload:hover::before {
  background-color: #3865B0;
  border: none;
  border-color: transparent;
}
.btn_upload:active::before {
  background-color: #3865B0;
}

.fileForm{
  position: absolute;
  width: 837px;
  height: 393px;
  left: 277px;
  top: 147px;
  background: #FFFFFF;
}

div.file-listing{
  width: 400px;
  margin: auto;
  padding: 10px;
  border-bottom: 1px solid #ddd;
}

div.file-listing img{
  height: 100px;
}

a.submit-button{
  display: block;
  margin: auto;
  text-align: center;
  width: 200px;
  padding: 10px;
  text-transform: uppercase;
  background-color: #CCC;
  color: white;
  font-weight: bold;
  margin-top: 20px;
}
</style>

<template>
  <div id="file-drag-drop">
    <form ref="fileform" class="fileForm">
      <div class="inp_label">
            <label class="dropzone-label grid place-items-center w-full h-full pt-10 pb-12 cursor-pointer" for="dropzone-file">
              <svg xmlns="http://www.w3.org/2000/svg" width="40" height="40" fill="currentColor" class="pointer-events-none text-current dropzone-label-icon bi bi-upload" viewBox="0 0 16 16">
                <path d="M.5 9.9a.5.5 0 0 1 .5.5v2.5a1 1 0 0 0 1 1h12a1 1 0 0 0 1-1v-2.5a.5.5 0 0 1 1 0v2.5a2 2 0 0 1-2 2H2a2 2 0 0 1-2-2v-2.5a.5.5 0 0 1 .5-.5z" />
                <path d="M7.646 1.146a.5.5 0 0 1 .708 0l3 3a.5.5 0 0 1-.708.708L8.5 2.707V11.5a.5.5 0 0 1-1 0V2.707L5.354 4.854a.5.5 0 1 1-.708-.708l3-3z" />
              </svg>
              <div class="dropzone-label-text">
                <p class="m-3 text-center">
                    Drag and drop files to upload
                </p>
              </div>
              <input type="file" class="btn btn_upload" @change="previewFiles"/>
            </label>
          </div>
    </form>
  </div>
</template>

<script>
	import Vue from 'vue'
	import axios from 'axios'

	Vue.use({
		install (Vue) {
			Vue.prototype.$api = axios.create({
				baseURL: 'http://localhost:8080/api/'
			})
		}
	})
  export default {
    data(){
      return {
        dragAndDropCapable: false,
        files: [],
        uploadPercentage: 0
      }
    },

    mounted(){

      this.dragAndDropCapable = this.determineDragAndDropCapable();

      if( this.dragAndDropCapable ){

        ['drag', 'dragstart', 'dragend', 'dragover', 'dragenter', 'dragleave', 'drop'].forEach( function( evt ) {

          this.$refs.fileform.addEventListener(evt, function(e){
            e.preventDefault();
            e.stopPropagation();
          }.bind(this), false);
        }.bind(this));

        this.$refs.fileform.addEventListener('drop', function(e){
          for( let i = 0; i < e.dataTransfer.files.length; i++ ){
            this.files.push( e.dataTransfer.files[i] );
          }

          this.onClickButton();
        }.bind(this));
      }
    },

    methods: {

      previewFiles(event) {
        for( let i = 0; i < event.target.files.length; i++ ){
          this.files.push( event.target.files[i] );
        }

        this.onClickButton();
      },

      onClickButton () {
        this.$emit('previewTrigger', this.files)
      },

      determineDragAndDropCapable(){

        var div = document.createElement('div');

        return ( ( 'draggable' in div )
                || ( 'ondragstart' in div && 'ondrop' in div ) )
                && 'FormData' in window
                && 'FileReader' in window;
      },

      submitFiles(){

        let formData = new FormData();

        for( var i = 0; i < this.files.length; i++ ){
          let file = this.files[i];

          formData.append('files[' + i + ']', file);
        }

        axios.post( '/file-drag-drop-instant',
          formData,
          {
            headers: {
                'Content-Type': 'multipart/form-data'
            },
            onUploadProgress: function( progressEvent ) {
              this.uploadPercentage = parseInt( Math.round( ( progressEvent.loaded * 100 ) / progressEvent.total ) );
            }.bind(this)
          }
        ).then(function(){
          console.log('SUCCESS!!');
        })
        .catch(function(){
          console.log('FAILURE!!');
        });
      },

      getImagePreviews(){

        for( let i = 0; i < this.files.length; i++ ){

          if ( /\.(jpe?g|png|gif)$/i.test( this.files[i].name ) ) {

            let reader = new FileReader();

            reader.addEventListener("load", function(){
              this.$refs['preview'+parseInt( i )][0].src = reader.result;
            }.bind(this), false);

            reader.readAsDataURL( this.files[i] );
          }else{

            this.$nextTick(function(){
              this.$refs['preview'+parseInt( i )][0].src = '/images/file.png';
            });
          }
        }
      },
    }
  }
</script>