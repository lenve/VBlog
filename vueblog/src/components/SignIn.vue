<template>
  <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="80px" class="sign_from">
  <el-form-item label="账号" prop="username">
    <el-input v-model="ruleForm.username"></el-input>
  </el-form-item>
  <el-form-item label="用户名" prop="nickname">
    <el-input v-model="ruleForm.nickname"></el-input>
  </el-form-item>
  <el-form-item label="密码" prop="password">
    <el-input type="password" v-model="ruleForm.password" autocomplete="off"></el-input>
  </el-form-item>
  <el-form-item label="确认密码" prop="checkPass">
    <el-input type="password" v-model="ruleForm.checkPass" autocomplete="off"></el-input>
  </el-form-item>
  <el-form-item label="邮箱" prop="email">
    <el-input v-model="ruleForm.email"></el-input>
  </el-form-item>
  <el-form-item>
    <el-button type="primary" @click="onSubmit">注册</el-button>
    <el-button @click="back" >返回</el-button>
  </el-form-item>
  </el-form>
</template>
<script>
  import {postRequest} from '../utils/api'
  import {putRequest} from '../utils/api'
  export default{
   data() {
        var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请输入密码'));
        } else {
          if (this.ruleForm.checkPass !== '') {
            this.$refs.ruleForm.validateField('checkPass');
          }
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请再次输入密码'));
        } else if (value !== this.ruleForm.password) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      };
      return {
        ruleForm: {
          username: '',
          nickname: '',
          password: '',
          checkPass:'',
          email: ''
        },
         rules: {
          username: [
            { required: true, message: '请输入账号', trigger: 'blur' },
            { min: 3, max: 64, message: '长度在 3 到 64 个字符', trigger: 'blur' }
          ],
             nickname: [
            { required: true, message: '请输入用户名', trigger: 'blur' },
            { min: 1, max: 64, message: '长度在 1 到 64 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true,validator: validatePass, trigger: 'blur' },
            { min: 6, max: 64, message: '密码长度必须在 6 到 64 个字符', trigger: 'blur' }
          ],
          checkPass: [
            { required: true,validator: validatePass2, trigger: 'blur' },
            { min: 6, max: 64, message: '密码长度必须在 6 到 64 个字符', trigger: 'blur' }
          ],
          email:[
            { required: true, message: '请输入邮箱地址', trigger: 'blur' },
            { type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur', 'change'] },
          ]
        }
      }
    },
    methods: {
      onSubmit:function() {
        var _this = this;
        this.loading = true;
        //前台数据验证
        //...
        postRequest('/reg', {
          username:  _this.ruleForm.username,
          password: _this.ruleForm.password,
          nickname: _this.ruleForm.nickname,
          email: _this.ruleForm.email
        }).then(resp=> {
          _this.loading = false;
          if (resp.status == 200) {
            //成功
            var json = resp.data;
            if (json.status == 'success') {
              _this.$alert('注册成功!', '成功!');
              _this.$router.replace({path: '/',query:{username:_this.ruleForm.username,password:_this.ruleForm.password}});
            } else {
              _this.$alert(json.msg, '失败!');
            }
          } else {
            //失败
            _this.$alert('注册失败!', '失败!');
          }
        }, resp=> {
          _this.loading = false;
          _this.$alert('找不到服务器⊙﹏⊙∥!', '失败!');
        });
      },
      back:function(){
         var _this = this;
        _this.$router.replace({path: '/'});
      }
    }
  }
</script>
<style>
@import url("//unpkg.com/element-ui@2.8.2/lib/theme-chalk/index.css");

.sign_from{
    padding-left: 33%;
    height: 400px;
    width: 30%;
}
</style>
