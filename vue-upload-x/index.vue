<template>
  <div id="UploadContainer">
    <ul class="picList">
      <li v-for="(val, key) in pictureList" :key="key">
        <img :src="val" class="pic" />
        <div class="ctrl">
          <button class="preBtn" @click="previewFn(val)">预览</button>
          <button class="selBtn" @click="delPicFn(key)">删除</button>
        </div>
      </li>
      <!-- 上传进度，依赖接口，随后支持 -->
      <!-- <li style="position: relative;background: #eee;" v-show="loadProgressStatus">
        <div class="uploadProgress">
          <p class="txt">{{progressPercent}}</p>
          <div class="progressBox">
            <p class="loaded" :style="{width: progressPercent}"></p>
          </div>
        </div>
      </li>-->
      <li class="PicruresBtn iconfont icon-add" v-if="currentPicLength < maxlength">
        <input type="file" class="PicruresFileInput" :accept="accept" :multiple="multiple" @change="uploadPicFn($event)" />
      </li>
    </ul>
    <div class="blackBg" :class="{'fade': previewBool}">
      <div class="previewBg" :class="{'aniFade': previewBool}">
        <img :src="preViewSrc" class="preview" />
        <button class="closeBtn" @click="closePreviewFn"></button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "",
  props: {
    pictureList: {
      type: Object,
      required: false,
      default: {} // 传入的图片数据 ({[id]: url} => eg: {12: 'www.abc.com/m.jpg'})
    },
    accept: {
      type: String,
      required: false,
      default: "image/gif, image/jpeg, image/jpg, image/png" // 限制上传图片的格式
    },
    limit: {
      type: String,
      required: false,
      default: 5 // 图片大小限制，不传默认为5M
    },
    maxlength: {
      type: String,
      required: false,
      default: 1000 // 限制上传图片的数量，超过将隐藏上传按钮
    },
    multiple: {
      type: Boolean,
      required: false,
      default: false // 是否可以多张上传
    },
    callbackDataType: {
      type: String,
      required: false,
      default: "base64" // 上传成功的回传数据类型，base64 || formData
    }
    // progressPercent: {
    //   type: String,
    //   required: false,
    //   default: 0 // 上传进度显示
    // }
  },
  data() {
    return {
      preViewSrc: "",
      previewBool: false
      // loadProgressStatus: false
    };
  },
  computed: {
    currentPicLength() {
      return Object.keys(this.pictureList).length;
    }
  },
  methods: {
    // 预览图片
    previewFn(imgSrc) {
      this.preViewSrc = imgSrc;
      this.previewBool = true;
    },
    // 关闭预览图
    closePreviewFn() {
      this.previewBool = false;
    },
    // 上传图片
    uploadPicFn(e) {
      let file = e.target;
      let reader = [];
      let _this = this;
      let maxSize = this.limit * 1024 * 1024;
      let formData = new FormData();
      let callbackData = []; // 回传数据，base64的时候使用
      let promise = []; // onload 队列
      //判断大小
      for (let i = 0; i < file.files.length; i++) {
        if (file.files[i].size > maxSize) {
          this.$toast(`上传图片大于${this.limit}M，请重新上传`, 3000);
          return false;
        }
        formData.append("file", e.target.files[i]);
      }
      if (this.callbackDataType === "formData") {
        // 回传数据
        this.$emit("upload", formData);
      } else {
        // 转码为base64
        for (let i = 0; i < file.files.length; i++) {
          // _this.loadProgressStatus = true;
          promise[i] = new Promise((resolve, reject) => {
            reader[i] = new FileReader();
            reader[i].readAsDataURL(file.files[i]);
            reader[i].onload = function(evt) {
              callbackData.push(evt.target.result);
              resolve();
            };
          });
        }
        Promise.all(promise).then(()=>{
          this.$emit("upload", callbackData.length === 1 ? callbackData[0] : callbackData);
        });
      }
      file.value = null; // 清空重置
    },
    // 提交上传图片
    PicruresImgFn(imgData) {},
    // 删除图片
    delPicFn(id) {
      this.$emit("delete", id);
    }
  }
};
</script>

<style scoped>
#UploadContainer .picList {
  overflow: hidden;
  margin: 20px 0 30px 0;
}

#UploadContainer .picList > li {
  float: left;
  width: 100px;
  height: 100px;
  border-radius: 4px;
  position: relative;
  margin: 0 8px 8px 0;
  cursor: pointer;
  box-sizing: border-box;
  background-color: #eee;
  overflow: hidden;
}

#UploadContainer .picList .pic {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  border-radius: 6px;
}

#UploadContainer .picList .ctrl {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 0;
  background-color: rgba(0, 0, 0, 0.5);
  border-radius: 6px;
  text-align: center;
  overflow: hidden;
  transition: all 0.5s ease;
  -webkit-transition: all 0.5s ease;
  -ms-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  text-align: center;
  box-sizing: border-box;
}

#UploadContainer .picList > li:hover .ctrl {
  height: 100%;
}

#UploadContainer .picList .ctrl > button {
  margin-top: 30%;
  display: inline-block;
  width: 36px;
  height: 26px;
  line-height: 26px;
  background-color: #2b89ff;
  font-size: 12px;
  color: #fff;
  border-radius: 4px;
}

#UploadContainer .PicruresBtn {
  line-height: 100px;
  text-align: center;
  background: #fff url("./addIco.png") no-repeat center;
  background-size: 26% auto;
  border-radius: 6px;
  font-size: 40px;
  font-weight: bold;
  position: relative;
  overflow: hidden;
}

#UploadContainer .PicruresBtn .PicruresFileInput {
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  cursor: pointer;
}

#UploadContainer .blackBg {
  overflow-y: auto;
  padding: 50px 0;
  box-sizing: border-box;
  opacity: 0;
  transition: all 0.5s ease;
  -webkit-transition: all 0.5s ease;
  -ms-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
  z-index: -9;
}

#UploadContainer .fade {
  opacity: 1;
  z-index: 999;
}

#UploadContainer .previewBg {
  margin: 30px auto 50px;
  width: 50%;
  height: auto;
  padding: 40px 20px 20px;
  box-sizing: border-box;
  background-color: #ddd;
  position: relative;
  transition: all 0.5s ease;
  -webkit-transition: all 0.5s ease;
  -ms-transition: all 0.5s ease;
  -moz-transition: all 0.5s ease;
}

#UploadContainer .aniFade {
  margin-top: 50px;
}

#UploadContainer .previewBg .closeBtn {
  position: absolute;
  right: 10px;
  top: 10px;
  width: 30px;
  height: 30px;
  background: url("./closeIco.png") no-repeat right 0;
  background-size: 20px auto;
}

#UploadContainer .preview {
  display: block;
  width: 100%;
  height: auto;
}
</style>