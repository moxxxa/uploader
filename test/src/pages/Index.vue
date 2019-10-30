<template>
  <q-page class="flex flex-center">
    <q-input v-model="number" label="how many time to upload the document"/>
    <q-uploader
      ref="fileUploader"
      url="http://localhost:4444/upload"
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
	  maxIterations: 2,
      name :'',
      type: '',
      size: '',
      number: 0
    }
  },
  methods: {
    addedFile (files) {
	  if (++this.iteration >= this.maxIterations) {
		this.$refs.fileUploader.upload()
		return
	  }
	  this.$refs.fileUploader.addFiles([new File(files, `${this.iteration}_${files[0].name}`)])
    },
    finishedUploading () {
      console.log('finiched uploading')
    },
    removeFile () {
      console.log('file removed')
      this.$refs.fileUploader.reset()
      this.iteration = 0
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
