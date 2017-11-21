<template>
  <div class="upload-wrapper">
    <div class="imgItem" v-show="imgSrcList.length>0" v-for="(imgSrc,index) in imgSrcList" :key="index">
      <img :src="imgSrc">
      <i class="icon-chahao" @click="delOne(index)"></i>
    </div>
    <div class="file" v-show="imgSrcList.length<maxLength">
      <input type="file" class="myfile" ref="file" @change="getFileUrl">
    </div>
  </div>
</template>

<script type='text/ecmascript-6'>
  export default {
    props: {
      maxLength: {
        type: Number,
        default: 6
      },
      imgSrcList: {
        type: Array,
        default: () => {
          return []
        }
      }
    },
    methods: {
      getFileUrl() {
        let file = this.$refs.file.files[0]
        this.$emit('uploadFile', file)
      },
      delOne(index) {
        this.$emit('uploadFileDel', index)
      }
    }
  }
</script>

<style scoped lang="stylus" rel="stylesheet/stylus">

  .upload-wrapper
    .imgItem
      box-sizing border-box
      width 33.33%
      height 80px
      display inline-block
      overflow hidden
      text-align center
      position relative
      margin 20px 0
      padding 0 20px
      img
        max-width 100%
      .icon-chahao
        display inline-block
        right 0
        top 0
        width 20px
        height 20px
        background url("./img/chahao.png") no-repeat
        background-size 100% 100%
        extend-click()
        position absolute
    .file
      width 24%
      height 80px
      display inline-block
      background url("./img/upload.png") no-repeat
      background-size 100% 100%
      margin 20px 10px
      vertical-align top
      .myfile
        border: none !important
        height 100%
        width 100%
        outline none
        opacity: 0
        &::-webkit-file-upload-button
          width: 1rem
          height: 1rem
          position: absolute
          outline: 0
          opacity: 0
</style>
