<template>
<div class="picture-uploader-wrapper">
  <el-upload :limit="limit || 99" :action="postUrl" :name="postName" :accept="acceptType" :on-remove="handleRemove" :on-success="handleSuccess">
    <el-button slot="trigger" type="success" plain size="mini">选择文件</el-button>
    <div slot="tip" class="el-upload__tip">只能上传 jpg/png 文件</div>
  </el-upload>
</div>
</template>

<script>
export default {
  name: 'imageUploader',
  props: ['limit'],
  data () {
    return {
      acceptType: 'image/jpeg,image/png',
      postUrl: 'http://pic.mashiro.wang/backend.php',
      postName: 'postimage'
    }
  },
  methods: {
    handleRemove: function (file, fileList) {
      this.$store.dispatch('status/removeUploadImage', { imageUrl: file.response.url })
    },
    handleSuccess: function (response, file, fileList) {
      if (response.status === 'OK') {
        this.$store.dispatch('status/pushUploadImage', { imageUrl: response.url })
      }
    }
  },
  created () {
    this.$store.dispatch('status/clearUploadImages')
  }
}
</script>

<style lang="scss" scoped>
.picture-uploader-wrapper {
  border: 1px solid #ddd;
  padding: 15px;
  border-radius: 4px;
}
</style>
