<template>
  <div>
      <el-form label-width="100px">
          <el-form-item label="封面" class="avatar-item">
          <div class="avatar-div">
                <img :src="form.coverImg" alt="" class="small-img" v-if="form.coverImg">
                <div class="null-img" v-else></div>
                <el-upload
                  :action="imgUpPath"
                  name="coverFile"
                  :headers="uploadHeader"
                  :on-success="onSuccess"
                  :show-file-list="false"
                >
                  <el-button>上传</el-button>
                </el-upload>
          </div>
        </el-form-item>
        <el-form-item label="文章标题">
          <el-input v-model="form.title" clearable="" placeholder="请输入文章标题"></el-input>
        </el-form-item>
        <el-form-item label="文章描述">
          <el-input v-model="form.desc" clearable="" placeholder="请输入文章描述"></el-input>
        </el-form-item>
        <el-form-item label="文章内容">
          <div id="editor"></div>
        </el-form-item>
        <el-form-item label="文章类别">
          <el-col :span="6">
            <el-input v-model="form.stemfrom" clearable="" placeholder="请输入文章类别"></el-input>
          </el-col>
        </el-form-item>
        <el-form-item label="文章ID">
          <el-col :span="6">
            <el-input v-model="form.id" clearable="" placeholder="请输入文章ID"></el-input>
          </el-col>
        </el-form-item>
        <el-form-item label="创建时间">
          <el-col :span="6">
            <el-input v-model="form.createTime" clearable="" placeholder="请输入创建时间"></el-input>
          </el-col>
        </el-form-item>
        <el-form-item label="作者">
          <el-col :span="6">
            <el-input v-model="form.author" clearable="" placeholder="请输入创建时间"></el-input>
          </el-col>
        </el-form-item>
        <el-form-item>
          <el-button type='primary' round @click="submit">发布文章</el-button>
        </el-form-item>
      </el-form>
  </div>
</template>

<script>
import Editor from 'wangeditor'
export default {
  data () {
    return {
      uploadHeader: {
        authorization: "Bearer " + localStorage.token,
      },
      imgUpPath: '',//封面上传地址
      form: {
        id: '',
        createTime: '',
        title: '',
        desc: '',
        stemfrom: '原创',
        author: this.$store.state.user.username,
        coverImg: ''
      },
      editor: null
    }
  },
  created(){
    this.imgUpPath = 'http://localhost:3000'+'/upload/cover/img'
  },
  mounted(){
      //创建wangEditor实例
      this.editor = new Editor('#editor')
      //配置上传图片的接口地址
      this.editor.config.uploadImgServer = `http://localhost:3000/upload/editor/img`
      this.editor.config.uploadFileName = 'editorFile'
      this.editor.config.uploadImgHeaders = {
        authorization: "Bearer " + localStorage.token
      }
      //设置富文本编辑器高度
      this.editor.config.height = 600
      //设置提示文字
      this.editor.config.placeholder = '编辑文章内容'
      this.editor.create()
      //初始值
      let date = new Date()
      this.form.id = Date.now()
      this.form.createTime = `${date.getFullYear()}-${date.getMonth()+1}-${date.getDate()} ${date.getHours()}:${date.getMinutes()}:${date.getSeconds()}`
  },
  methods: {
    onSuccess(res){
      console.log(res)
      this.form.coverImg = res.path//上传成功显示图片预览
    },
    submit(){
       //获取文章内容
      let content = this.editor.txt.html()
      let params = {...this.form,content:content}
      console.log('params',params)
      this.$http({
        path: '/article/add',
        method: 'post',
        params: params
      }).then(res=>{
        if(res.data.code === 200){
          this.$router.push({
              path: "/admin/article"
          });
        }
      })
    }
  },
}
</script>

<style scoped lang="less">
</style>
