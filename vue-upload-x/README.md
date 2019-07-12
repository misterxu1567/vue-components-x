> 基于vue的上传图片预览组件

<br/><br/>
<img src="https://raw.githubusercontent.com/misterxu1567/img-static/master/upload.png" alt="上传图片预览组件预览" width="200">

### NPM

``` bash
npm install vue-upload-x --save-dev
```
### Example

```
<template>
    <div>
        <UploadX
        :pictureList="pictureList"
        limit="2"
        accept="image/gif, image/jpeg, image/jpg, image/png"
        maxlength="2"
        multiple
        callbackDataType='formData'
        @upload="uploadFn"
        @delete="deletePicFn"
        ></UploadX>
    </div>
</template>
<script>
    import UploadX from "vue-upload-x";

    export default {
        name: "App",
        components: {
            UploadX
        },
        data() {
            return {
            pictureList: {
                17: "https://img.zcool.cn/community/0155f45535fea40000001e31083bfa.jpg@1280w_1l_2o_100sh.jpg"
            }
            };
        },
        mounted() {},
        methods: {
            // 上传
            uploadFn(imgData) {
                console.log(imgData)
            },
            // 删除
            deletePicFn(id) {
            console.log(id)
            }
        }
    };
</script>
```

## Api
### 参数
| Name                 | Type      | Default      | Description                                                        |
|----------------------|-----------|--------------|--------------------------------------------------------------------|
| pictureList          | `Object`  | `{}`         | 初始化传入的图片数据，格式：{id: url}         |
| limit                | `String`  | `5`          | 限制大小限制，单位（M）  |
| accept               | `String`  | `image/gif, image/jpeg, image/jpg, image/png`   | 上传文件类型限制             |
| maxlength            | `String`  | `1000`       | 上传图片张数限制             |
| multiple             | `Boolean` | `false`      | 是否允许多图上传             |
| callbackDataType     | `String`  | `base64`     | 本地拿到图片数据的回调参数，支持 formData && base64             |
| upload               | `Function`| 'null'     | 本地拿到图片数据的回调回调函数             |
| delete               | `Function`| 'null'     | 触发删除的回调函数             |