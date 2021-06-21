<template>
<div class="justify-content-center file_drap_inp">
        <div class="fileForm" v-bind:style="{ left: leftWrapper, width: widthWrapper }">
                <video autoplay  src="../../assets/62669-success-lottie-animation.mp4"></video>
                <div class="successText">
                    Upload Sucessful
                </div>
        </div>
</div>
</template>

<script>
export default{
    name: 'UploadSucess',
    props: ['widthWrapper', 'leftWrapper'],
    components: {
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
video{
    display: inline;
    margin-top: 5%;
    height: 200px;
    width: 200px;
}
.successText{
    font-size: 20px;
}
</style>