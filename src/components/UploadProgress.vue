<template>
<div>
	<UploadSuccess v-if="successShow" :widthWrapper="widthWrapper" 
        :leftWrapper="leftWrapper"/>
 <div class="justify-content-center file_drap_inp" v-if="!successShow">
        <div class="fileForm" v-bind:style="{ left: leftWrapper, width: widthWrapper }">
    <div class="large-12 medium-12 small-12 cell">
      <br>
      <progress max="100" :value.prop="uploadPercentage" :data-label.prop="uploadPercentage">Uploading {{this.uploadPercentage}}%</progress>
      <br>
    </div>
	<div class="UploadPercent">
		<p>
			Uploading {{this.uploadPercentage}}%
		</p>
	</div>
  </div>
 </div>
</div>
</template>

<style>

progress {
	position: absolute;
	content: attr(data-label);
	margin-top: 20%;
    border: 0;
	left: 22%;
	width: 70%;
    height: 30px;
    border-radius: 20px;
	
}
progress::-webkit-progress-bar {
    border: 0;
    height: 30px;
	width: 80%;
    border-radius: 20px;
	background-color: #e0e0e0;
}
progress::-webkit-progress-value {
    border: 0;
    height: 30px;
	width: 80%;
    border-radius: 20px;
	background-color: rgba(56, 101, 176, 0.46);
}
progress::-moz-progress-bar {
    border: 0;
    height: 30px;
	width: 80%;
    border-radius: 20px;
}
.UploadPercent{
	position: absolute;
	top: 50%;
	left: 42%
}
</style>

<script>
/* eslint-disable no-mixed-spaces-and-tabs */
	import Vue from 'vue'
	import axios from 'axios'
	import UploadSuccess from "./UploadSuccess.vue"

	Vue.use({
		install (Vue) {
			Vue.prototype.$api = axios.create({
				baseURL: '/api/'
			})
		}
	})
	export default {
		props: ['files', 'widthWrapper', 'leftWrapper'],
		data(){
			return {
				uploadPercentage: 0,
				successShow: false, 
			}
		},

		components: {
			UploadSuccess
		},

		mounted() {
			this.submitFiles();
		},

		methods: {
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
						if (this.uploadPercentage==100) {
							this.successShow = true;
						}
					}.bind(this)
				}
				).then(function(){
				})
				.catch(function(){
				});
			},	
		}	
  	}
/* eslint-enable no-mixed-spaces-and-tabs */
</script>