<template>
  <div id="register" v-title data-title="注册 - HZ-博客">
    <video preload="auto" class="me-video-player" autoplay="autoplay" loop="loop" muted="muted">
          <source src="static/vedio/sea.mp4" type="video/mp4">
    </video>

    <div class="me-login-box me-login-box-radius">
      <h1>HZ-博客 注册</h1>

      <el-form ref="userForm" :model="userForm" :rules="rules">
        <el-form-item prop="account" label="用户名">
          <el-input placeholder="用户名" v-model="userForm.account"></el-input>
        </el-form-item>

        <el-form-item prop="nickname" label="昵称">
          <el-input placeholder="昵称" v-model="userForm.nickname"></el-input>
        </el-form-item>

        <el-form-item prop="password" label="密码">
          <el-input placeholder="密码" type="password" v-model="userForm.password"></el-input>
        </el-form-item>

        <el-form-item size="small" class="me-login-button">
          <el-button type="primary" @click.native.prevent="register('userForm')">注册</el-button>
        </el-form-item>
        <el-form-item size="small" class="me-login-button">
          <el-button type="info" @click.native.prevent="backHome">返回主页</el-button>
        </el-form-item>
<!--        <el-form-item  class="me-login-button" >-->
<!--          <el-switch-->
<!--            v-model="value"-->
<!--            active-text="打开音乐"-->
<!--            inactive-text="关闭音乐"-->
<!--            active-color="#13ce66"-->
<!--            inactive-color="#ff4949"-->
<!--            style="display: block"-->
<!--            @click.native="changeMusic"-->
<!--          >-->
<!--          </el-switch>-->
<!--        </el-form-item>-->

      </el-form>



    </div>
  </div>
</template>

<script>
  import {register} from '@/api/login'

  export default {
    name: 'Register',
    data() {
      return {
        userForm: {
          account: '',
          nickname: '',
          password: '',
        },
        value: true,
        rules: {
          account: [
            {required: true, message: '请输入用户名', trigger: 'blur'},
            {max: 10, message: '不能大于10个字符', trigger: 'blur'}
          ],
          nickname: [
            {required: true, message: '请输入昵称', trigger: 'blur'},
            {max: 10, message: '不能大于10个字符', trigger: 'blur'}
          ],
          password: [
            {required: true, message: '请输入密码', trigger: 'blur'},
            {max: 10, message: '不能大于10个字符', trigger: 'blur'}
          ]
        }

      }
    },
    methods: {
      register(formName) {
        let that = this
        this.$refs[formName].validate((valid) => {
          if (valid) {

            that.$store.dispatch('register', that.userForm).then(() => {
              that.$message({message: '注册成功 快写文章吧', type: 'success', showClose: true});
              that.$router.push({path: '/'})
            }).catch((error) => {
              if (error !== 'error') {
                that.$message({message: error, type: 'error', showClose: true});
              }
            })

          } else {
            return false;
          }
        });

      },
      backHome(){
        this.$router.push("/");
        this.$message({
          message: '取消注册',
          type: 'warning',
          showClose:true
        });
      }

    }
  }
</script>

<style scoped>
  #login {
    min-width: 100%;
    min-height: 100%;

  }

  .me-video-player {
    background-color: transparent;
    width: 100%;
    height: 100%;
    object-fit: fill;
    display: block;
    position: absolute;
    left: 0;
    z-index: 0;
    top: 0;
  }

  .me-login-box {
    position: absolute;
    width: 300px;
    height: 440px;
    background-color: white;
    margin-top: 150px;
    margin-left: -180px;
    left: 50%;
    padding: 30px;
  }

  .me-login-box-radius {
    border-radius: 10px;
    box-shadow: 0px 0px 1px 1px rgba(161, 159, 159, 0.1);
  }

  .me-login-box h1 {
    text-align: center;
    font-size: 24px;
    margin-bottom: 20px;
    vertical-align: middle;
  }

  .me-login-design {
    text-align: center;
    font-family: 'Open Sans', sans-serif;
    font-size: 18px;
  }

  .me-login-design-color {
    color: #5FB878 !important;
  }

  .me-login-button {
    text-align: center;
  }

  .me-login-button button {
    width: 100%;
  }

</style>
