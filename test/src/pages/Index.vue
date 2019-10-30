<template>
  <q-page class="flex flex-center">
    <q-input v-model="number" label="how many time to upload the document"/>
    <q-uploader
      ref="fileUploader"
      url="http://localhost:4444/upload"
      @added="addedFile"
      @finish="finishedUploading"
      @removed="removeFile"
      hide-upload-button
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
      name :'',
      type: '',
      size: '',
      number: 0
    }
  },
  methods: {
    addedFile (files) {
      console.log('file name :', files[0].name)
      const file = new File([files[0]], files[0].name)
      console.log('original =', files[0]);
      console.log('************')
      console.log('copie =',  file);
      //  console.log('file uploader =', this.$refs.fileUploader)
      this.uploadFile(file)
    },
    async uploadFile (file) {
      if (this.iteration < this.number) {
        let fileArray =[]
        console.log('iteration numero :', this.iteration);
        this.$refs.fileUploader.upload()
        console.log('1');


        setTimeout(() => {
          this.$refs.fileUploader.removeUploadedFiles()
        }, 400);
        console.log('11');


        setTimeout(() => {
          let fileFinal = new File([fileFinal], file.name)
          fileArray.push(fileFinal)
        }, 600);
        console.log('111');


        setTimeout(() => {
          if (this.iteration < this.number) {
            this.$refs.fileUploader.addFiles(fileArray)
          } else {
            this.$refs.fileUploader.reset()
            this.iteration = 0
          }
        }, 700);
        //  this.$refs.fileUploader.addFiles(file)
        console.log('1111')
      // console.log('file uploader =', this.$refs.fileUploader.__getFileInput())
      this.iteration += 1
      }
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
