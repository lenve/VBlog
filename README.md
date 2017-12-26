V部落是一个多用户博客管理平台，采用Vue+SpringBoot开发。  

项目演示地址： [http://45.77.146.32:8081/index.html](http://45.77.146.32:8081/index.html)  

# 项目效果图  

## 登陆页面

![登录](http://github.com/lenve/VBlog/raw/master/doc/login.png)  

## 文章列表

![文章列表](http://github.com/lenve/VBlog/raw/master/doc/article.png)  

## 发表文章

![发表文章](http://github.com/lenve/VBlog/raw/master/doc/post.png)  

## 用户管理

![用户管理](http://github.com/lenve/VBlog/raw/master/doc/usermana.png)  

## 栏目管理

![栏目管理](http://github.com/lenve/VBlog/raw/master/doc/category.png)  

## 数据统计

![数据统计](http://github.com/lenve/VBlog/raw/master/doc/datastatistics.png)  

# 技术栈  

## 后端技术栈

后端主要采用了：  

1.SpringBoot  
2.SpringSecurity  
3.MyBatis  
4.部分接口遵循Restful风格  
5.MySQL  

## 前端技术栈

前端主要采用了：  

1.Vue  
2.axios  
3.ElementUI  
4.vue-echarts  
5.mavon-editor  
6.vue-router  

还有其他一些琐碎的技术我就不在这里一一列举了。   

# 快速运行  

1.克隆本项目到本地  

```
git@github.com:lenve/VBlog.git
```  

2.找到blogserver项目中resources目录下的vueblog.sql文件，在MySQL数据库中执行  
3.根据自己本地情况修改数据库配置，数据库配置在SpringBoot项目的application.properties中  
4.在IntelliJ IDEA中运行blogserver项目  

**OK，至此，服务端就启动成功了**  

5.进入到vueblog目录中，在控制台依次输入如下命令：  

```
# 安装依赖
npm install

# 在 localhost:8080 启动项目
npm run dev
```  

项目启动之后，在浏览器中输入http://localhost:8080就可以访问了。  


**步骤5中需要大家对NodeJS、NPM等有一定的使用经验，不熟悉的小伙伴可以先自行搜索学习下，推荐Vue[官方教程](https://cn.vuejs.org/v2/guide/)。**  


# 项目依赖  

1.[vue-echarts](https://github.com/Justineo/vue-echarts)  
2.[mavonEditor](https://github.com/hinesboy/mavonEditor)  

# License

MIT

**欢迎小伙伴们star、fork。**  

关注公众号查看更多全栈资料：  

![公众号二维码](http://github.com/lenve/VBlog/raw/master/doc/qrcode.png)  