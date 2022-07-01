<script lang="ts" setup>
import Editor from '@tinymce/tinymce-vue'
import {ref} from "vue";

//双向绑定编辑器数据
const input_content = ref("")
//tinymce选项配置
const initOptions = ref({
  //挂载点
  selector: '#edit_input',
  //语言设置
  language: "zh-Hans",
  //编辑器区域自定义样式
  content_style: "img {max-width:100%;}",
  //插件配置
  plugins: 'print preview searchreplace autolink directionality visualblocks visualchars fullscreen image link media template advcode codesample table charmap hr pagebreak nonbreaking anchor insertdatetime advlist lists wordcount imagetools textpattern help emoticons autosave bdmap indent2em autoresize formatpainter axupimgs importword kityformula-editor',
  //工具栏配置
  toolbar1: 'code undo redo restoredraft | cut copy paste pastetext | forecolor backcolor bold italic underline strikethrough link anchor | alignleft aligncenter alignright alignjustify outdent indent | \
                     styleselect formatselect fontselect fontsizeselect | bullist numlist | blockquote subscript superscript removeformat ',
  toolbar2:'table image media charmap emoticons hr pagebreak insertdatetime print preview | fullscreen | bdmap indent2em lineheight formatpainter axupimgs importword kityformula-editor',
  //菜单栏配置
  menubar:false,
  //宽高设置
  width: '100%',
  height: '100%',
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
  flex-direction: column;
  border: 2px solid yellow;
  #edit_input{
    width: 100%;
    flex-grow: 10;
    align-self: stretch;
    border: 2px solid red;
  }
}
</style>

