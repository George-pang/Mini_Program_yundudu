<template>
  <div class="card-container">
      <div class="bg"></div>
      <div class="form-box">
          <div class="form">
              <div class="form-item input-item" v-for="item in inputList" :key="item.id">
                <div class="item-left">
                      {{ item.title }}
                </div>
                <div class="item-right">
                      <input type="text" :placeholder="item.text" v-model="item.value">
                      <div class="yzm-btn" v-if="item.flag" @click="getYzm">
                        获取验证码
                      </div>
                </div>
              </div>
              <div class="form-item confirm-item">
                <div class="confirm-btn" @click="submit">
                  确认
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
      inputList:[
        {id:1,value:"",flag:false,title:"持卡人",text:"请输入持卡人姓名"},
        {id:2,value:"",flag:false,title:"卡号",text:"请输入卡号"},
        {id:3,value:"",flag:false,title:"手机号",text:"请输入绑定银行卡的手机号"},
        {id:4,value:"",flag:true,title:"验证码",text:"请输入验证码"},
      ]
    }
  },
  methods: {
      getYzm: function() {
      if (this.inputList[2].value === "") {
        wx.showToast({
          title: "请您输入绑定银行卡的手机号！",
          icon: "none",
          duration: 1500
        });
        return false;
      }else if(!(/^1[34578]\d{9}$/.test(this.inputList[2].value))){
        wx.showToast({
          title: "您的手机号格式输入错误,请重新输入！",
          icon: "none",
          duration: 1500
        });
        return false;
      }else{
        wx.showToast({
          title: "验证码已发送，请注意查收!",
          icon: "none",
          duration: 1500
        });
        return false;
      }
    },
      submit: function() {
        if (this.inputList[0].value === "") {
          //微信API--显示消息提示框
          wx.showToast({
            title: "请输入持卡人姓名！", //提示的内容
            icon: "none",
            duration: 1500
          });
          return false;
        }else if(!(/^[\u4E00-\u9FA5\uf900-\ufa2d·s]{2,20}$/.test(this.inputList[0].value))){
          wx.showToast({
            title: "请输入真实的姓名！",
            icon: "none",
            duration: 1500
          });
          return false;
        }

        if (this.inputList[1].value === "") {
          wx.showToast({
            title: "请输入银行卡号！",
            icon: "none",
            duration: 1500
          });
          return false;
        }

        if (this.inputList[2].value === "") {
          wx.showToast({
            title: "请输入绑定银行卡的手机号！",
            icon: "none",
            duration: 1500
          });
          return false;
        }else if(!(/^1[34578]\d{9}$/.test(this.inputList[2].value))){
          wx.showToast({
            title: "您的手机号格式输入错误,请重新输入！",
            icon: "none",
            duration: 1500
          });
          return false;
        }

        if (this.inputList[3].value === "") {
          wx.showToast({
            title: "请输入验证码！",
            icon: "none",
            duration: 1500
          });
          return false;
        }

        wx.redirectTo({
          url: '/pages/bind_success/main'
        })
      }

  },

  created () {

  }
}
</script>

<style scoped>
  .card-container{
    position: relative;
    height: 100vh;
    background-color: #f8f8f8;
  }
  .bg{
    height: 285rpx;
    background-color: #ff563f;
  }
  .form-box{
    position: absolute;
    top: 93rpx;
    left: 0;
    width: 100%;
    padding: 0 16px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .form-box .form{
    padding: 0 16px;
    background-color: #fff;
    box-shadow: 0px 1px 7px 0px
    rgba(0, 0, 0, 0.2);
    border-radius: 5px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .form .form-item{
    height: 50px;
    min-width: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .form-item .item-left{
    font-size: 16px;
    letter-spacing: 0px;
    color: #333333;
    width: 60px;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .form-item .item-right{
    flex: 1;
    min-width: 0;
    margin-left: 10px;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .form-item .item-right>input{
    flex: 1;
    font-size: 16px;
    letter-spacing: 0px;
    color: #999999;
    text-align: right;
  }
  .input-item{
    position: relative;
  }
  .input-item::after{
    content: '';
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background-color: #eeeeee;
  }
  .input-item .yzm-btn{
    position: relative;
    margin-left: 30px;
    font-size: 16px;
    letter-spacing: 0px;
    color: #ff563f;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .input-item .yzm-btn::before{
    content: "";
    position: absolute;
    left: -15px;
    top: 50%;
    transform: translateY(-50%);
    height: 32px;
    width: 1px;
    background-color: #eeeeee;
  }
  .confirm-item{
    justify-content: flex-end!important;
  }
  .confirm-item .confirm-btn{
    height: 31px;
    padding: 0 30px;
    font-size: 16px;
    letter-spacing: 0px;
    color: #feffff;
    background-color: #ff563f;
    border-radius: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
</style>
