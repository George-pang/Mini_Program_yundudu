<template>
  <div class="login-container">
    <div class="login-ch">
      <img src="/static/img/chahua.png" alt="" mode="widthFix">
    </div>
    <div class="l-r-box">
      <img src="/static/img/bg.png" alt="" mode="widthFix">
      <div class="l-r-container">
          <div class="sayhi">
            <div class="chaiquan">
              <img src="/static/img/chaiquan.png" alt="" mode="widthFix">
            </div>
            <div class="hi">
              Hi，欢迎来到云笃笃
            </div>
          </div>
          <div class="l-r-btn">
            <div class="r-btn" @click="showrTc">注册</div>
            <div class="l-btn" @click="showlTc">登录</div>
          </div>
      </div>
    </div>

    <!--注册弹窗-->
    <div class="tc-register-box" v-show="flag1">
      <div class="box">
        <div class="content-box">
          <div class="logo">
            <img src="/static/img/logo.png" alt="" mode="widthFix">
          </div>
          <div class="form-box">
            <div class="form-item">
              <input type="text" id="nameInput" placeholder="请输入姓名" v-model="name"/>
            </div>
            <div class="form-item">
              <input type="text" id="telInput" placeholder="请输入手机号" v-model="phone1"/>
            </div>
            <div class="form-item">
              <picker @bindchange="bindPickerChange" :value="index" :range="array" class="picker-box">
                <view class="picker">
                  选择行业：{{array[index]}}
                </view>
              </picker>
            </div>
            <div class="zc-btn" @click="registerHandle">
              注册
            </div>
            <div class="close-btn" @click="closerTc">
              <img src="/static/img/close.png" alt="" mode="widthFix">
            </div>
          </div>
        </div>
      </div>
    </div>
    <!--登录弹窗-->
    <div class="tc-login-box" v-show="flag2">
      <div class="box">
        <div class="content-box">
          <div class="logo">
            <img src="/static/img/logo.png" alt="" mode="widthFix">
          </div>
          <div class="form-box">
            <div class="form-item">
              <input type="text" id="dl-telInput" placeholder="请输入手机号" v-model="phone2"/>
            </div>
            <div class="form-item get-dtm">
              <input type="text" id="dtmInput" placeholder="请输入动态码" v-model="dtm"/>
              <div class="dtm-btn">
                获取动态码
              </div>
            </div>
            <div class="dl-btn" @click="loginHandle">
              登录
            </div>
            <div class="close-btn" @click="closelTc">
              <img src="/static/img/close.png" alt="" mode="widthFix">
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      array: ['搜索引擎营销', '网建', '非企', '百科', '负面', '微信开发', '其他'],
      flag1: false,
      flag2: false,
      index: 0,
      name: '',
      phone1: '',
      phone2: '',
      dtm: ''
    }
  },
  methods: {
    bindPickerChange: function (e) {
      console.log('picker发送选择改变，携带值为', e.detail.value)
      this.setData({
        index: e.detail.value
      })
    },
    showrTc: function () {
      this.flag1 = !this.flag1
      console.log('111')
    },
    showlTc: function () {
      this.flag2 = !this.flag2
    },
    closerTc: function () {
      this.flag1 = false
    },
    closelTc: function () {
      this.flag2 = false
    },
    registerHandle: function () {
      if (this.name === '') {
        wx.showToast({
          title: "请输入您的姓名",
          icon: "none",
          duration: 1500
        });
        return false;
      }else if(!(/^[\u4E00-\u9FA5\uf900-\ufa2d·s]{2,20}$/.test(this.name))){
        wx.showToast({
          title: "请输入真实的姓名",
          icon: "none",
          duration: 1500
        });
        return false;
      }

      if (this.phone1 ===''){
        wx.showToast({
          title: "请输入您的手机号",
          icon: "none",
          duration: 1500
        });
        return false;
      }else if(!(/^1[34578]\d{9}$/.test(this.phone1))){
        wx.showToast({
          title: "您的手机号输入有误,请重新输入",
          icon: "none",
          duration: 1500
        });
        return false;
      }
        wx.showToast({
          title: "注册成功！",
          icon: "none",
          duration: 1500
        });
        this.flag1=false;
        this.flag2=true;
        this.name='';
        this.phone1=''
    },
    loginHandle: function() {
      if (this.phone2 === '') {
        wx.showToast({
          title: "请输入手机号",
          icon: "none",
          duration: 1500
        });
        return false;
      }else if(!(/^1[34578]\d{9}$/.test(this.phone2))){
        wx.showToast({
          title: "您的手机号输入有误,请重新输入",
          icon: "none",
          duration: 1500
        });
        return false;
      }
      if (this.dtm === '') {
        wx.showToast({
          title: "请输入动态码",
          icon: "none",
          duration: 1500
        });
        return false;
      }
      wx.redirectTo({
        url: '/pages/index/main'
      });
      this.flag1=false;
      this.flag2=false;
      this.phone2='';
      this.dtm=''
    }
  },
}
</script>

<style scoped>
  .login-container{
    height: 100vh;
    padding-top: 55px;
    display: flex;
    flex-direction: column;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .login-ch{
    display: flex;
    justify-content: center;
  }
  .login-ch img{
      width: 300px;
      vertical-align: top;
  }
  .l-r-box{
      position: relative;
      flex: 1;
      background-image: url("/static/img/bg.png");
  }
  .l-r-box img{
    width: 100%;
    vertical-align: top;
  }
  .l-r-container{
    position: absolute;
    top: 80px;
    left: 50%;
    width: 100%;
    padding: 0 30px;
    transform: translateX(-50%);
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .sayhi{
    display: flex;
    min-width: 0;
  }
  .sayhi .chaiquan{
    margin-left: 15px;
  }
  .sayhi .chaiquan img{
    width: 80px;
    vertical-align: top;
  }
  .sayhi .hi{
    font-family: JWaWAZuan;
    font-size: 24px;
    line-height: 1em;
    letter-spacing: 0;
    color: #ffffff;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .l-r-btn{
    margin-top: -6px;
    width: 100%;
    display: flex;
  }
  .l-r-btn .r-btn,.l-r-btn .l-btn{
    flex: 1;
    height: 43px;
    line-height: 43px;
    font-size: 18px;
    border: solid 1px #ffffff;
    text-align: center;
    /*display: flex;*/
    /*!*justify-content: center;*!*/
    /*align-items: center;*/
  }
  .l-r-btn .r-btn,.l-r-btn .l-btn{
    color: #ffffff;
    border-radius: 22px 0 0 22px;
  }
  .l-r-btn .l-btn{
    color: #ff6752;
    background-color: #fff;
    border-radius: 0 22px 22px 0;
  }
  /*弹窗*/
  .tc-register-box,.tc-login-box{
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    /*display: none;*/
    padding: 0 16px;
    background-color: rgba(0, 0, 0, 0.4);
    z-index: 999;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .box{
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
    width: 100%;
    padding: 0 16px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .content-box{
    position: relative;
    width: 100%;
    padding: 15px 16px 30px;
    background-color: #ffffff;
    border-radius: 10px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .content-box .logo{
    display: flex;
    justify-content: center;
  }
  .content-box .logo img{
    width: 60px;
    vertical-align: top;
  }
  .form-box{

  }
  .form-box .form-item{
    margin-top: 15px;
    height: 45px;
    padding: 0 16px;
    background-color: #f8f8f8;
    border-radius: 22px;
  }
  .form-item >input{
    width: 100%;
    height: 100%;
    font-size: 16px;
    letter-spacing: 0;
    color: #999999;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .form-item .picker-box{
    width: 100%;
  }
  .form-item .picker-box .picker{
    height: 45px;
    line-height: 45px;
    font-size: 16px;
    letter-spacing: 0;
    color: #333;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .zc-btn,.dl-btn{
    margin-top: 30px;
    height: 45px;
    line-height: 45px;
    text-align: center;
    background-color: #ff563f;
    border-radius: 22px;
    font-size: 18px;
    color: #ffffff;
  }
  .close-btn{
    position: absolute;
    right: 12px;
    top: 12px;
  }
  .close-btn img{
    width: 25px;
    vertical-align: top;
  }
  .get-dtm{
    display: flex;
  }
  .get-dtm .dtm-btn{
    font-size: 16px;
    letter-spacing: 0;
    color: #ff563f;
    white-space: nowrap;
    align-self: center;
  }
</style>
