# upload-img

> A Vue component

- 传入 maxLength(最多上传的图片张数)、imgSrcList(需要显示的url数组)
- 向外派发 uploadFile(上传文件)、uploadFileDel(删除的图片的index)


父组件：

    <img-upload
          @uploadFile="uploadFile"
          @uploadFileDel="uploadFileDel"
          :imgSrcList="imgSrcList"
          :maxLength="maxLength"
        ></img-upload>

    export default {
        data() {
          return {
            fileList: [],   // 上传文件列表
            imgSrcList: [],  // 显示的图片url数组
            maxLength: 3
          }
        },
        methods: {
          uploadFile(file) {
          // 此处也可以进行ajax上传，由后端返回图片线上地址，进行操作
            let reader = new FileReader()
            reader.readAsDataURL(file)
            reader.onloadend = (e) => {
             this.imgSrcList.push(e.target.result)
              this.fileList.push(file)
            }
          },
          uploadFileDel(index) {
            this.imgSrcList.splice(index, 1)
            this.fileList.splice(index, 1)
          }
        },
        components: {
          ImgUpload
        }
    }
