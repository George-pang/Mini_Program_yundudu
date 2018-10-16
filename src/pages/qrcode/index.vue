<template>
  <div class="qr-container">
    <div class="qr-wrapper">
      <div class="qr-box">
        <div class="title-row">
          <div class="title">
            扫一扫，加入我的团队
          </div>
          <button class="share-btn" @click="sharePage" open-type="share" plain="true">
            <div class="share-icon">
              <img src="/static/img/share.png" alt="" mode="widthFix">
            </div>
            <div class="share-txt">
              分享
            </div>
          </button>
        </div>
        <div class="qrcode">
          <img src="/static/img/erweima1.png" alt="" mode="widthFix">
        </div>
      </div>
    </div>
    <div class="share-to-box" v-show="flag">
      <div class="box-title">
        分享到
      </div>
      <div class="share-list">
        <div class="share-item" v-for="item in shareList" :key="item.id">
          <div class="item-icon">
            <img :src="item.url" alt="" mode="widthFix">
          </div>
          <div class="item-name">
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="close-btn" @click="flag=false">
        <img src="/static/img/close.png" alt="" mode="widthFix">
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      flag: false,
      shareList: [
        {id:1,url:"/static/img/pyq.png",name:"朋友圈"},
        {id:2,url:"/static/img/weixin.png",name:"微信"},
        {id:3,url:"/static/img/qq.png",name:"QQ"},
        {id:4,url:"/static/img/weibo.png",name:"微博"},
      ]
    }
  },
  methods: {
    sharePage: function() {
      this.flag=true;
    }
  },
  //mpvue兼容的小程序生命周期钩子
  onShareAppMessage: function() {
    return {
      //自定义转发标题
      title: "扫一扫，加入我的团队！"
    };
  },
  created () {

  }
}
</script>

<style scoped>
  .qr-container{
    height: 100vh;
    background-color: #f8f8f8;
    font-family: HiraginoSansGB-W3;
  }
  .qr-wrapper{
    padding: 60px 16px 0;
  }
  .qr-box{
    padding: 20px 34px;
    background-color: #ffffff;
    box-shadow: 0 1px 7px 0
    rgba(0, 0, 0, 0.2);
    border-radius: 5px;
  }
  .title-row{
    display: flex;
    justify-content: space-between;
  }
  .title-row .title{
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0;
    color: #333333;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .title-row .share-btn{
    display: flex;
    align-items: center;
    margin: 0;
    background-color: #fff;
    padding: 0;
  }
  button[plain]{ border:0 }
  .share-btn .share-icon{
    display: flex;
    align-items: center;
  }
  .share-btn .share-icon img{
    width: 17px;
    vertical-align: middle;
  }
  .share-btn .share-txt{
    margin-left: 5px;
    font-size: 14px;
    line-height: 1em;
    letter-spacing: 0;
    color: #999999;
  }
  .qrcode{
    margin-top: 20px;
  }
  .qrcode img{
    width: 275px;
    vertical-align: top;
  }

  .share-to-box{
    position: fixed;
    bottom: 0;
    left: 0;
    width: 100%;
    padding: 15px 35px 34px;
    background-color: #ffffff;
    border-radius: 5px 5px 0 0;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .box-title{
    text-align: center;
    font-size: 18px;
    line-height: 1em;
    letter-spacing: 0px;
    color: #333333;
  }
  .share-list{
    margin-top: 20px;
    display: flex;
    justify-content: space-between;
  }
  .share-list .share-item{
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .share-item .item-icon img{
    width: 50px;
    vertical-align: top;
  }
  .share-item .item-name{
    margin-top: 12px;
    font-size: 14px;
    line-height: 1em;
    letter-spacing: 0;
    color: #666666;
  }
  .close-btn{
    position: absolute;
    top: 12px;
    right: 20px;
  }
  .close-btn img{
    width: 25px;
    vertical-align: top;
  }
</style>
