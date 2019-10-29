<template>
  <q-page class="flex flex-center">
    <q-uploader
      ref="fileUploader"
      url="http://localhost:4444/upload"
      @added="addedFile"
      @finish="finishedUploading"
      @removed="removeFile"
      hide-upload-button
    />
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      attachment: null,
      backup: null
    }
  },
  methods: {
    addedFile (files) {
      console.log('file name :', files[0].name)
      // let file1 = new File([files[0]], files[0].name)
      // let file2 = new File([files[0]], files[0].name)
      // let file3 = new File([files[0]], files[0].name)
      // let file4 = new File([files[0]], files[0].name)
      // let totalFile = []
      // totalFile.push(file1)
      // totalFile.push(file2)
      // totalFile.push(file3)
      // totalFile.push(file4)
      // console.log('totalFile =', totalFile)
      // this.$refs.fileUploader.addFiles(totalFile)
      this.uploadFile(files)
    },
    async uploadFile (files) {
      let i = 0
      while (i < 5) {
        i += 1
        await setTimeout(() => {
          this.$refs.fileUploader.upload()
        }, 10)
        await setTimeout(() => {
          this.$refs.fileUploader.reset()
        }, 2000)
        await setTimeout(() => {
          this.$refs.fileUploader.addFiles(new File([files[0]], files[0].name))
        }, 200)
      }
    },
    finishedUploading () {
      console.log('finiched uploading')
    },
    removeFile () {
      console.log('file removed')
    }
  }

}
</script>
