# qiniu-upload-vue
一个七牛上传用于vue的包
========================
1，在项目中执行以下命令
```
npm install qiniu-upload-vue

```
2,示例代码
```
 <upload 
      :uptoken='uptoken'   //这是从后端获取的七牛token 可以参考另一项目laravel后端提供token[laravelQiniu]:https://github.com/liumingsongning/laravelQiniu
      :filename='filename' //自定义上传文件前缀，因为七牛上传是不分目录的，定义了这个变量上传后效果大体是这样'http://www.baidu.com/filename/原文件名
      browse_button='pickfiles' //指定上传按钮id，随便定义
      domain='http://p8htjuaac.bkt.clouddn.com' //七牛提供的domain
      bucket_name='huijin'  //七牛你自己设置的参数
      @on-percente="filePercent"  //这是子组件传回的上传进度参数，filPercent是你自己需要定义的，必须在methods中定义此方法
      @on-change="UploadComplete"> //这是子组件传回的上传完成后完整文件路径，UploadComplete是你自己需要定义的，必须在methods中定义此方法
      <Button type="ghost" id="pickfiles" slot='button'>选择文件</Button> //随便定义一个插槽，slot='button'必须写上，id与上面的browse_button一致
      <Progress slot='progressBar'></Progress>//随便定义一个插槽，slot='progressBar'必须写上，显示进度用，子组件传回的进度参数在 @on-percente="filePercent"中国获得
  </upload>
  //js部分
  //导入
  import Upload from "qiniu-upload-vue";
  
  data () {
      return {
          uptoken:'',
          filename:'', 
      }
  },
  mounted() {
      let _this = this;
      this.ajax
      .get("/test")  //此路由后台代码参考[laravelQiniu]:https://github.com/liumingsongning/laravelQiniu
      .then(function(response) {
          _this.uptoken = response.data.token;
      })
      .catch(function(error) {
          console.log(error);
      });
   methods: {
      UploadComplete(val){
        console.log(val);
      },
      filePercent(val){
         console.log(val);
      }
    }
  },
  ```
  
  
