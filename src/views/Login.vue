<template>
    <div class="login-wrap">
        <el-form
        class="login-form"
        label-position="top"
        label-width="80px"
        :model="formData">
          <h3>用户登录</h3>
          <el-form-item label="用户名">
            <el-input v-model="formData.username"></el-input>
          </el-form-item>
          <el-form-item label="密码">
            <el-input type="password" v-model="formData.password"></el-input>
          </el-form-item>
          <el-form-item>
            <el-button class="login-btn" type="primary" @click="handleLogin">登录</el-button>
          </el-form-item>
        </el-form>
    </div>
</template>
<script>
export default {
  data() {
    return {
      formData: {
        username: '',
        password: ''
      }
    };
  },
  methods: {
    handleLogin() {
      this.$http
        .post('login', this.formData)
        .then((response) => {
          // console.log(response);
          const { meta: { msg, status } } = response.data;
          if (status === 200) {
            this.$message.success(msg);
            sessionStorage.setItem('token', response.data.data.token);
            // this.$router.push('/login');
          } else {
            this.$message.error(msg);
          }
        })
        .catch((err) => {
          console.log(err);
        });
    }
  }
};
</script>
<style>
  .login-wrap {
    height: 100%;
    background-color: #324152;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  .login-form {
    width: 500px;
    background-color: #fff;
    padding: 30px;
    border-radius: 5px;
  }
  .login-btn {
    width: 100%;
  }
</style>
