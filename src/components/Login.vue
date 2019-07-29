<template>
  <body id="poster">
  <el-form class="login-container" label-position="left"
           label-width="0px">
    <h3 class="login_title">系统登录</h3>
    <el-form-item>
      <el-input type="text" v-model="loginForm.username"
                auto-complete="off" placeholder="账号"></el-input>
    </el-form-item>
    <el-form-item>
      <el-input type="password" v-model="loginForm.password" @keyup.enter.native="login"
                auto-complete="off" placeholder="密码"></el-input>
    </el-form-item>
    <el-form-item style="width: 100%">
      <el-button type="primary" style="width: 100%;background: #505458;border: none" v-on:click="login">登录</el-button>
    </el-form-item>
    <el-form-item style="width: 100%">
      <el-button type="primary" style="width: 100%;background: #505458;border: none" v-on:click="registryForm">注册
      </el-button>
    </el-form-item>
  </el-form>

  <el-dialog
    title="注册"
    :visible.sync="dialogFormVisible"
    @close="clear">
    <el-form v-model="form" style="text-align: left" ref="dataForm">
      <el-form-item label="昵称" :label-width="formLabelWidth">
        <el-input v-model="form.account" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="用户名" :label-width="formLabelWidth">
        <el-input v-model="form.username" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="密码" :label-width="formLabelWidth">
        <el-input v-model="form.password" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="邮箱" :label-width="formLabelWidth">
        <el-input v-model="form.email" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item label="性别" :label-width="formLabelWidth">
        <el-radio-group v-model="form.gender">
          <el-radio label="男"></el-radio>
          <el-radio label="女"></el-radio>
        </el-radio-group>
      </el-form-item>
    </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="registry">确 定</el-button>
    </div>
  </el-dialog>

  </body>
</template>


<script>
  export default {
    name: "Login",
    data() {
      return {
        formLabelWidth: '120px',
        dialogFormVisible: false,
        loginForm: {
          username: '',
          password: ''
        },
        responseResult: [],
        form: {
          id: '',
          username: '',
          password: '',
          email: '',
          account: '',
          gender: '',
          avatar: '',
          enable: '',
          regTime: '',
          createTime: '',
          updateTime: ''
        }
      }
    },
    methods: {
      login() {
        this.$axios.post('/login', {
          username: this.loginForm.username,
          password: this.loginForm.password
        })
          .then(successResponse => {
            if (successResponse.data.code === 200) {
              this.$router.replace({path: '/index'})
            }
          })
          .catch(failResponse => {
          })
      },
      clear() {
        this.form = {
          username: '',
          password: '',
          email: '',
          account: '',
          gender: ''
        }
      },
      registryForm() {
        this.dialogFormVisible = true
      },
      registry() {
        this.$axios.post('/registry', {
          username: this.form.username,
          password: this.form.password,
          email: this.form.email,
          account: this.form.account,
          gender: this.form.gender,
          avatar: this.form.avatar,
          enable: this.form.enable,
          regTime: this.form.regTime,
          createTime: this.form.createTime,
          updateTime: this.form.updateTime,
        }).then(successResponse => {
          if (successResponse && successResponse.status === 200) {
            this.dialogFormVisible = false
          }
        }).catch(error => {
          console.log(error.response)
        });

      }
    }
  }
</script>

<style>
  .login-container {
    border-radius: 15px;
    background-clip: padding-box;
    margin: 90px auto;
    width: 350px;
    padding: 35px 35px 15px 35px;
    background: #fff;
    border: 1px solid #eaeaea;
    box-shadow: 0 0 25px #cac6c6;
  }

  .login_title {
    margin: 0px auto 40px auto;
    text-align: center;
    color: #505458;
  }

  #poster {
    background: url("../assets/lake.jpg") no-repeat;
    background-position: center;
    height: 100%;
    width: 100%;
    background-size: cover;
    position: fixed;
  }

  body {
    margin: 0px;
  }


</style>

