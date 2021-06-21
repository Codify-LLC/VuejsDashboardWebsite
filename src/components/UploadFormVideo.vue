<template>
    <div class="justify-content-center file_drap_inp">
        <div class="fileForm" v-bind:style="{ left: leftWrapper, width: widthWrapper }">
            <div v-for="(file, key) in files" v-bind:key="key">
                <video autoplay class="preview VideoUpload" alt="" v-bind:ref="'preview'+parseInt( key )"/>
            </div>
            <form class="uploadForm" @submit.prevent="onClickButton">
                <input type="text" class="titleUpload" placeholder="Title*" required/>
                 <textarea type="text" class="DescriptionUpload" placeholder="Description" required/>
                 <input type="text" class="CommunityUpload" placeholder="Select The Community*" required/>
                 <input type="text" class="TagUpload" placeholder="Tag*" required/>
                 <button class="BtnUpload" type="submit" v-show="files.length > 0">Upload</button>
            </form>
        </div>
    </div>
    
</template>
<script>
export default{
    name: 'UploadFormVideo',
    props: ['files', 'widthWrapper', 'leftWrapper'],
    mounted() {
        this.getVideoPreviews();
    },
    methods: {
        getVideoPreviews(){

        for( let i = 0; i < this.files.length; i++ ){

          if ( /\.(mp4|mkv)$/i.test( this.files[i].name ) ) {

            let reader = new FileReader();

            reader.addEventListener("load", function(){
              this.$refs['preview'+parseInt( i )][0].src = reader.result;
            }.bind(this), false);

            reader.readAsDataURL( this.files[i] );
          }else{

            this.$nextTick(function(){
              this.$refs['preview'+parseInt( i )][0].src = '/videos/file.mp4';
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
.VideoUpload{
    position: absolute;
    width: 404px;
    height: 217px;
    left: 50px;
    top: 50px;
}
.titleUpload{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 60px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}
.DescriptionUpload{
    position: absolute;
    width: 270px;
    height: 70px;
    right: 70px;
    top: 110px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}
.CommunityUpload{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 195px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}

.TagUpload{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 245px;
    background: #F7F7F7;
    border: 1px solid #C8C8C8;
    box-sizing: border-box;
    border-radius: 5px;
}
.BtnUpload{
    position: absolute;
    width: 270px;
    height: 35px;
    right: 70px;
    top: 295px;
    background-color: #3865B0;
    box-sizing: border-box;
    border-radius: 5px;
    outline: none;
    color: white;
    border: 0px solid black;
}
</style>