<template>
  <el-row class="container">
    <el-col :span="12" class="header">
      <div class="title">V部落博客管理平台</div>
    </el-col>
    <el-col :span="12" class="header">
      <div class="userinfoContainer">
        <el-dropdown @command="handleCommand">
  <span class="el-dropdown-link userinfo">
    {{currentUserName}}<i class="el-icon-arrow-down el-icon--right userinfo"></i>
  </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item command="sysMsg">系统消息</el-dropdown-item>
            <el-dropdown-item command="MyArticle">我的文章</el-dropdown-item>
            <el-dropdown-item command="MyHome">个人主页</el-dropdown-item>
            <el-dropdown-item command="logout" divided>退出登录</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </div>
    </el-col>
    <el-col :span="24" style="height: 100%;">
      <el-container>
        <el-aside width="200px">
          <el-menu
            default-active="0"
            class="el-menu-vertical-demo" style="background-color: rgba(0, 0, 0, 0.08)">
            <el-submenu index="1">
              <template slot="title">
                <i class="el-icon-location"></i>
                <span>导航一</span>
              </template>
              <el-menu-item index="1-1" style="background-color: rgba(0, 0, 0, 0.04)">选项1</el-menu-item>
              <el-menu-item index="1-2" style="background-color: rgba(0, 0, 0, 0.04)">选项2</el-menu-item>
              <el-menu-item index="1-3" style="background-color: rgba(0, 0, 0, 0.04)">选项3</el-menu-item>
            </el-submenu>
            <el-menu-item index="2">
              <i class="el-icon-menu"></i>
              <span slot="title">导航二</span>
            </el-menu-item>
            <el-menu-item index="3">
              <i class="el-icon-setting"></i>
              <span slot="title">导航三</span>
            </el-menu-item>
          </el-menu>
        </el-aside>
        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-col>
  </el-row>
</template>
<script>
  export default{
    methods: {
      handleCommand(command){
        var _this = this;
        if (command == 'logout') {
          this.$confirm('注销登录吗?', '提示', {
            confirmButtonText: '确定',
            cancelButtonText: '取消',
            type: 'warning'
          }).then(function () {
            _this.$http.get("/logout");
            _this.currentUserName = '游客';
            _this.$router.replace({path: '/'});
          }, function () {
            //取消
          })
        }
      }
    },
    mounted: function () {
      this.$http.get("/currentUserName").then(function (msg) {
        this.currentUserName = msg.bodyText;
      }, function (msg) {
        this.currentUserName = '游客';
      });
    },
    data(){
      return {
        currentUserName: ''
      }
    }
  }
</script>
<style>
  .container {
    position: absolute;
    top: 0px;
    left: 0px;
    width: 100%;
    background-color: rgba(235, 235, 235, 0.08);
  }

  .header {
    background-color: #20a0ff;
    height: 60px;
  }

  .title {
    color: #fff;
    font-size: 22px;
    display: flex;
    align-items: center;
    margin-left: 20px;
    height: 60px;
  }

  .userinfo {
    color: #fff;
    cursor: pointer;
  }

  .userinfoContainer {
    display: flex;
    align-items: center;
    justify-content: flex-end;
    height: 60px;
    margin-right: 20px;
  }
</style>
