<template>
  <q-page class="flex flex-center">
    <q-input v-model="number" label="how many time to upload the document"/>
    <q-uploader
      ref="fileUploader"
      :url="provideURL"
	  multiple
      @added="addedFile"
      @finish="finishedUploading"
      @removed="removeFile"
      hide-upload-button
	  class="n-uploader"
    />
      <div>
        &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
        {{iteration}}
      </div>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      attachment: null,
      backup: null,
      iteration: 0,
	  maxIterations: 3,
      name :'',
      type: '',
      size: '',
      number: 0,
      urls: ['http://localhost:4444/upload', 'http://localhost:4448/upload', 'http://localhost:4446/upload']
    }
  },
  methods: {
    addedFile (files) {
	  if (++this.iteration >= this.maxIterations) {
	  	sessionStorage.setItem('uploading_url_index', 0)
		this.$refs.fileUploader.upload()
		return
	  }
	  this.$refs.fileUploader.addFiles([new File(files, `_${files[0].name}`)])
    },
    finishedUploading () {
      console.log('finiched uploading')
    },
    removeFile () {
      console.log('file removed')
      this.$refs.fileUploader.reset()
      this.iteration = 0
    },
    provideURL () {
    	let uploading_url_index = Number(sessionStorage.getItem('uploading_url_index'))
    	sessionStorage.setItem('uploading_url_index', uploading_url_index + 1)
    	return this.urls[uploading_url_index]
    }
  }

}
</script>

<style>
.n-uploader div.q-uploader__file {
	display: none;
}
.n-uploader div.q-uploader__file:first-child {
	display: block;
}
</style>
