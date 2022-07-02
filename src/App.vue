<script lang="ts" setup>
import Editor from '@tinymce/tinymce-vue'
import {ref} from "vue";

//双向绑定编辑器数据
const input_content = ref("")
//tinymce选项配置
const initOptions = ref({
  //挂载点
  selector: '#edit_input',
  //模式
  // inline: true,
  //语言设置
  language: "zh-Hans",
  //自动聚焦
  auto_focus: true,
  //只读模式
  //readonly:true,
  //空内容时展示
  placeholder: '正文内容',
  //引入站外插件
  external_plugins: {},
  //解决缓存问题
  cache_suffix: '?v=1.0.0',
  //编辑器区域自定义样式
  content_style: "img {max-width:100%;}",
  //自定义图标
  //  icons_url: 'src/assets/tinymce/icons/custom/icons',
  // icons: 'custom',
  //插件配置
  plugins: ['wordcount','table','searchreplace','preview','pagebreak','insertdatetime','fullscreen','emoticons','codesample','charmap','autosave','autolink','anchor','advlist', 'autolink', 'image', 'lists', 'preview', 'code'],
  //工具栏配置
  toolbar1: 'forecolor backcolor|code|bullist|numlist|blockquote|styles|bold italic strikethrough underline|alignleft aligncenter alignright|subscript|superscript',
  toolbar2: 'table|searchreplace|preview|pagebreak|insertdatetime|fullscreen|emoticons|codesample|charmap|restoredraft|anchor|link image | language',
  //工具栏模式
  toolbar_mode:'sliding',
  //设置插件时间格式
  insertdatetime_formats: ["%H点%M分", "%Y年%m月%d日"],
  //保存在localstorage下的文件的保存时间
  autosave_retention:'10080m',
  //菜单栏配置
  menubar: false,
  //设置工具栏在顶部
  fixed_toolbar_container: '#edit_input',
  //宽高设置
  width: '100%',
  height: '100%',
  //设置皮肤
  skin: 'oxide',
  //主题设置
  theme:'silver',
  //编辑器大小改变
  resize: false,
  //隐藏状态栏底部图标
  branding: false,
  //init出多个实例时只在该实例上显示菜单栏（多个编辑器时很有用）
  // event_root: '#edit_input',
  //隐藏状态栏左侧路径
  elementpath: false,
  //允许代码保留注释
  allow_conditional_comments: true,
  //字体列表
  font_formats: '微软雅黑=Microsoft YaHei,Helvetica Neue,PingFang SC,sans-serif;苹果苹方=PingFang SC,Microsoft YaHei,sans-serif;宋体=simsun,serif',
  //指定图片上传接口
  images_upload_url: '/demo/upimg.php',//后端返回json应该是{ location : "/demo/image/1.jpg" }这种格式
  //指定图片上传返回的相对路径的基本路径
  images_upload_base_path: '/demo',
  //使用自己的方式处理图片上传
  /* images_upload_handler: function (blobInfo, succFun, failFun) {
     var xhr, formData;
     var file = blobInfo.blob();//转化为易于理解的file对象
     xhr = new XMLHttpRequest();
     xhr.withCredentials = false;
     xhr.open('POST', '/demo/upimg.php');
     xhr.onload = function() {
       var json;
       if (xhr.status != 200) {
         failFun('HTTP Error: ' + xhr.status);
         return;
       }
       json = JSON.parse(xhr.responseText);
       if (!json || typeof json.location != 'string') {
         failFun('Invalid JSON: ' + xhr.responseText);
         return;
       }
       succFun(json.location);
     };
     formData = new FormData();
     formData.append('file', file, file.name );//此处与源文档不一样
     xhr.send(formData);
   }*/
  //移动端适配
  mobile: {
    menubar: false,
  },
  //初始化前执行函数
  setup: function (editor) {
    console.log("ID为: " + editor.id + " 的编辑器即将初始化.");
  },
  //初始化后执行回调
  init_instance_callback: function (editor: Editor) {
    console.log("ID为: " + editor.id + " 的编辑器已初始化完成.");
  }
})



</script>

<template>
  <div class="edit_wrap">
    <Editor
        tabindex="1"
        v-model="input_content"
        id="edit_input"
        :init="initOptions"
    />
  </div>
</template>

<style lang="scss" scoped>
.edit_wrap {
  height: 100%;
  overflow: hidden;
  display: flex;
  #edit_input,#edit_outer {
    width: 100%;
    flex-grow: 10;
    align-self: stretch;
  }
}
</style>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body, html {
  height: 100vh;
}

#app {
  height: 100%;
}

img {
  max-width: 400px !important;
}

</style>
