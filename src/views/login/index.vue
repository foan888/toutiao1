<template>
  <div class="login">
      <!-- 表单 -->
      <el-card class="login-card">
      <!-- 表单内容 -->
      <!-- 头部logo部分 -->
      <div class="title">
        <img src="../../assets/img/logo_index.png" alt="">
      </div>
      <!-- 表单 绑定model属性 绑定rules属性（表单验证规则）-->
      <el-form ref="loginForm" :model="loginForm" :rules="loginRules" style="margin-top:20px">
          <!-- 表单容器 设置prop属性 prop表示要校验的字段名-->
          <el-form-item prop="mobile">
              <!-- 表单域 v-model双向绑定-->
              <el-input v-model="loginForm.mible" placeholder="请输入手机号"></el-input>
          </el-form-item>
          <!-- 验证码 -->
          <el-form-item prop="code">
              <el-input v-model="loginForm.code" style="width:60%" placeholder="请输入验证码"></el-input>
              <!-- 放按钮 -->
              <el-button style="float:right" plain>发送验证码</el-button>
          </el-form-item>
          <!-- 表单域 -->
          <el-form-item prop="checked">
              <!-- 霸王条款 是否同意被坑 -->
              <el-checkbox v-model="loginForm.checked">我已阅读同意用户协议和隐私条款</el-checkbox>
          </el-form-item>
          <!-- 按钮 -->
          <el-form-item>
              <el-button @click="login" style="width:100%" type="primary">登录</el-button>
          </el-form-item>
      </el-form>
      </el-card>
  </div>
</template>

<script>
export default {
  data () {
    return {
      // 登录表单的数据
      loginForm: {
        mobile: '', // 手机号
        code: '', // 验证码
        checked: false // 是否同意用户协议
      },
      // 定义表单的验证规则
      loginRules: {
        // required 如果为true 表示该字段必填
        mobile: [{ required: true, message: '您的手机号不能为空' }, {
          pattern: /^1[3-9]\d{9}$/, // 正则表达式
          message: '您的手机号格式不正确'
        }],
        code: [{ required: true, message: '您的验证码不能为空' }, {
          pattern: /^\d{6}$/,
          message: '您的验证码不正确'
        }],
        // 自定义校验 required不能校验true/false
        checked: [{
          validator: function (rule, value, callback) {
            // rule 是当前校验规则
            // value 当前要验证的字段值
            // callback 回调函数 不论成功否 都执行
            // 成功执行callback 失败执行 callback(new Error())
            // new Error(错误信息) 就是我们提示的错误信息
            value ? callback() : callback(new Error('您必须同意我们的霸王条款'))
          }
        }]
      }
    }
  },
  methods: {
    login () {
      // this.$refs.loginForm 获取就是el-form 的对象实例
    //   this.$refs.loginForm.validate(function (isOK) {
    //     if (isOK) {
    //         console.log("校验通过")
    //     } else {
    //         console.log("校验未通过")
    //     }
    //   }) // 方法
    // 第二种方式 promise
      this.$refs.loginForm.validate().then(() => {
        // 如果成功通过 校验就会到达 then
      })
    }
  }
}
</script>

<style lang='less' scoped>
// 只想对自己的组件起作用 加 scoped属性
// 如果需要写less style标签 加 lang="less"
    // h1 {
    //     color: red;
    // }
    // .login {
    //     h1 {
    //         color: red;
    //     }
    // }
    .login {
      background-image:- url(../../assets/img/02.jpg);
      // background-image: url(../../assets/img/back.jpg);
      height: 100vh;//当前可视区域分为100份
      background-size: cover;
      display: flex;
      justify-content: center;
      align-items: center;
      &:before {
        content: '123';
        width: 100%;
        height: 100%;
        position: absolute;
        background-image: url('../../assets/img/02.jpg');
        filter:blur(5px);
        background-size: cover;
      }
      .login-card {
          background: rgba(0,0,0,0);
          z-index: 2;
          width: 440px;
          height: 340px;
          .title {
              text-align: center;
              img {
                  height: 40px;
              }
          }
      }
    }
</style>
