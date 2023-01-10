<template>
  <div class="all">
    <div class="sufee-login d-flex align-content-center flex-wrap">
      <div class="container">
        <div class="login-content">
          <div class="login-logo">
            <a>
              <img
                class="align-content"
                src="../assets/img/yining_logo.png"
                alt=""
                style="position: absoult"
              />
            </a>
          </div>
          <div
            class="login-form"
            style="background-color: rgba(6, 7, 7, 0.4); border-radius: 16px"
          >
            <form
              id="loginForm"
              method="post"
              style="width: 90%; margin-left: 5%"
            >
              <div class="form-group">
                <label style="color: #fff">用户名</label>
                <input
                  type="text"
                  class="form-control"
                  id="username"
                  placeholder=""
                  name="username"
                  v-model="username"
                />
              </div>
              <div class="form-group">
                <label style="color: #fff">密码</label>
                <input
                  type="password"
                  class="form-control"
                  id="password"
                  placeholder=""
                  name="password"
                  v-model="password"
                />
              </div>

              <div class="checkbox">
                <label> <input type="checkbox" /> 记住密码 </label>
                <label class="pull-right">
                  <a onclick="alert('请联系管理员')" style="color: #ffcc33"
                    >忘记密码?</a
                  >
                </label>
              </div>
              
              <button
                id="btn_sub"
                type="button"
                class="btn btn-success btn-flat m-b-30 m-t-30"
                style="background-color: #4694e2"
                @click="login"
              >
                登 录
              </button>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
@import "../assets/css/bootstrap.min.css";
.bg-dark {
  background-color: #343a40 !important;
}
.all {
  height: 100%;
  background: url(../assets/img/login1.jpg);
  background-size: 100% 116%;
  transform: rotateY(360deg);
  display: table;
  font-family: "Open Sans", sans-serif;
  font-size: 16px;
  width: 100%;
}
.container {
  max-width: 1140px;
  height: 752px;
  width: 100%;
  /* height: 100%; */
  padding-right: 15px;
  padding-left: 15px;
  margin-right: auto;
  margin-left: auto;
}
.login-content {
  max-width: 540px;
  margin: 8vh auto;
}
.login-logo {
  text-align: center;
  margin-bottom: 15px;
}
img {
  max-width: 100%;
}
.login-form {
  background: #ffffff;
  padding: 30px 30px 20px;
  border-radius: 2px;
}
.form-group {
  margin-bottom: 1rem;
  margin-top: 1rem;
}
.login-form label {
  color: #878787;
  text-transform: uppercase;
}
label {
  display: inline-block;
  margin-bottom: 0.5rem;
}
.btn,
button,
input,
textarea {
  -webkit-box-shadow: none;
  box-shadow: none;
  outline: 0 !important;
}
.login-form .checkbox {
  color: #878787;
}
.login-form .checkbox label {
  text-transform: none;
}
.pull-right {
  float: right;
}
.login-form label a {
  color: #ff2e44;
}
.login-form .btn {
  width: 100%;
  text-transform: uppercase;
  font-size: 14px;
  padding: 15px;
  border: 0px;
}
.btn,
.button {
  display: inline-block;
  font-weight: 400;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  -webkit-transition: all 0.15s ease-in-out;
  transition: all 0.15s ease-in-out;
  border-radius: 3;
  cursor: pointer;
}
</style>
<script>
import axios from "axios";
// import elementUi from 'element-ui'
import { message } from 'ant-design-vue';
import { defineComponent } from 'vue';
export default {
  data() {
    return {
      username: "",
      password: "",
    };
  },

  methods: {
    login() {
      if (this.username == "") {
        message.warning('请输入用户名');
        return;
      } else if (this.password == "") {
        message.warning('请输入密码');
        return;
      }
      axios({
        url: "http://183.201.200.28:9002/user/login",
        method: "GET",
        params: {
          username: this.username,
          password: this.password,
        },
        headers: {
          "Content-Type": "application/json",
          access_token: this.token,
        },
      }).then((response) => {
        if (response.status == 200) {
          console.log(response);
          window.localStorage.setItem("token", response.data.data);
          console.log(response.data.data);
          if(response.data.message == '操作成功'){
            message.success('登陆成功!');
             this.$router.push({
                name:"Layout2"
            })
          }else if(response.data.message == '密码错误！'){
             message.error('密码错误！');
          }else if(response.data.message == '用户名不存在！'){
            message.warning('用户名不存在！');
          }
         
        }
      });
    },
  },
  // var xhr=new XMLHttpRequest();
  // xhr.open('POST', 'https://www.apifox.cn/apidoc/shared-21a47a84-4071-4873-956b-6d96bfea77a5/user/login', true);
  // xhr.setRequestHeader('Content-Type', 'application/json'); //请求头
  // xhr.send(JSON.stringify({ "username": this.username, "password": this.password}));
  // xhr.onload = function () {
  //   if (xhr.status == 200) {
  //     console.log("登录成功");
  //     localStorage.setItem("login", "true");
  //     localStorage.setItem("username", userLogins.value);
  //     window.location.href = "index.html";
  //   }else {
  //     console.log("账号不存在");
  //   }
  // }

  // }
  // }
};
</script>
