<template>
<div class="setting-form">
  <image-uploader/>
</div>
</template>

<script>
import ImageUploader from '../ImageUploader'
export default {
  name: 'updateAvatar',
  components: {
    ImageUploader
  },
  data () {
    return {
      imageUrl: ''
    }
  }
}
</script>

<style lang="scss">
.avatar-uploader .el-upload {
  border: 1px dashed #d9d9d9;
  border-radius: 6px;
  cursor: pointer;
  position: relative;
  overflow: hidden;

  &:hover {
    border-color: #409EFF;
  }
}

.avatar-uploader-icon {
  font-size: 28px;
  color: #8c939d;
  width: 178px;
  height: 178px;
  line-height: 178px;
  text-align: center;
}

.avatar {
  width: 178px;
  height: 178px;
  display: block;
}

</style>
