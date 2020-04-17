<template>
  <div class="login-container">
    <div class="login-box">
      <el-form class="login-form" :model="loginForm">
        <el-form-item>
          <el-input prefix-icon="el-icon-user-solid" v-model="loginForm.username"></el-input>
        </el-form-item>

        <el-form-item>
          <el-input prefix-icon="el-icon-search" type="password" v-model="loginForm.password"></el-input>
        </el-form-item>
      
        <el-form-item class="btns">
          <el-button type="primary" @click="login">登录</el-button>
          <el-button type="info">重置</el-button>
        </el-form-item>

      </el-form>
    </div>
  </div>
</template>

<script>
  export default {
    data () {
      return {
        loginForm:{
          username: 'admin',
          password: '123456'
        }
      }
    },
    methods: {
       async login() {
       this.$http.post("login", this.loginForm).then(resp => {
         const data = resp.data;
         if(data.meta.status !== 200) {
           this.$message.error("登录失败")
           return
         }
         this.$message.success("登录成功")

         console.log(data)
         window.sessionStorage.setItem("token", data.data.token)
         this.$router.push('/home')
       })
      
      }
    }
  }

</script>

<style lang="less" scoped>
  .login-container {
    background-color: #2b4b6b;
    height: 100%;
  }

  .login-box {
    width: 450px;
    height: 300px;
    background-color: #ffffff;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%)
  }

  .login-form {
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 20px;
    box-sizing: border-box
  }

// 按钮居右对齐
  .btns {
    display: flex;
    justify-content: flex-end;
  }

</style>>
