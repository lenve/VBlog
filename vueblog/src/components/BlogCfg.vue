<template>
  <el-card style="width: 500px" v-loading="loading">
    <div>
      <div style="text-align: left">
        <el-form :model="emailValidateForm" label-position="top" ref="emailValidateForm"
                 style="color:#20a0ff;font-size: 14px;">
          <el-form-item
            prop="email"
            label="开启博客评论通知"
            :rules="[{type: 'email', message: '邮箱格式不对哦!'}]">
            <el-input type="email" v-model.email="emailValidateForm.email" auto-complete="off" style="width: 300px"
                      placeholder="请输入邮箱地址..." size="mini"></el-input>
            <el-button type="primary" @click="submitForm('emailValidateForm')" size="mini">确定</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </el-card>
</template>
<script>
  import {getRequest} from '../utils/api'
  import {putRequest} from '../utils/api'
  export default{
    data(){
      return {
        emailValidateForm: {
          email: ''
        },
        loading: false
      }
    },
    mounted: function () {
      var _this = this;
      getRequest("/currentUserEmail").then(resp=> {
        if (resp.status == 200) {
          _this.emailValidateForm.email = resp.data;
        }
      });
    },
    methods: {
      submitForm(formName) {
        var _this = this;
        this.$refs[formName].validate((valid) => {
          if (valid) {
            _this.loading = true;
            putRequest("/updateUserEmail", {email: _this.emailValidateForm.email}).then(resp=> {
              _this.loading = false;
              if (resp.status == 200) {
                _this.$message({type: resp.data.status, message: resp.data.msg});
              } else {
                _this.$message({type: 'error', message: '开启失败!'});
              }
            }, resp=> {
              _this.loading = false;
              _this.$message({type: 'error', message: '开启失败!'});
            });
          } else {
            _this.$message({type: 'error', message: '邮箱格式不对哦!'})
            return false;
          }
        });
      }
    }
  }
</script>
