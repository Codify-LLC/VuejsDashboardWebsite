<template>
    <div class="justify-content-center file_drap_inp">
        <div class="dropzone-wrapper border-current border-dashed">
            <div v-for="(file, key) in files" v-bind:key="key">
                <img class="preview imgUpload" v-bind:ref="'preview'+parseInt( key )"/>
            </div>
            <form @submit.prevent="onClickButton" class="uploadForm">
                <textarea type="text" class="captionUpload" placeholder="Caption*" required/>
                 <input type="text" class="communityUploadImg" placeholder="Select The Community*" required/>
                 <button type="submit" class="btnUploadImg" v-show="files.length > 0">Upload</button>
            </form>
        </div>
    </div>
    
</template>
<script>
export default{
    name: 'UploadFormImg',
    props: ['files'],
    mounted() {
        this.getImagePreviews();
    },
    methods: {
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
      onClickButton () {
        this.$emit('uploadFile', this.files)
      },
    },
}
</script>
<style>

.dropzone-wrapper {
    position: absolute;
    width: 837px;
    height: 393px;
    left: 277px;
    top: 147px;
    background: #FFFFFF;
}
.imgUpload{
    position: absolute;
    width: 404px;
    height: 217px;
    left: 150px;
    top: 50px;
}
.captionUpload{
    position: absolute;
    width: 270px;
    height: 70px;
    right: 70px;
    top: 60px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}
.communityUploadImg{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 145px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}
.btnUploadImg{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 195px;
    background-color: #3865B0;
    box-sizing: border-box;
    border-radius: 5px;
    outline: none;
    color: white;
    border: 0px solid black;
}
</style>