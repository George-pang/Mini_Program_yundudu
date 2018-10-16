<template>
  <div class="index-container">
    <swiper class="swiper_container" autoplay="true" circular="true" interval="2000" v-show="flag1">
      <swiper-item v-for="item in inforList" :key="item.id">
				<div class="notice-icon">
					<img src="/static/img/notice.png" alt="" mode="widthFix">
				</div>
        <navigator :url="item.url" open-type="navigate">
            <view class="swiper_item">{{item.title}}</view>
        </navigator>
        <div class="close-btn" @click="closeSwiper">
          <img src="/static/img/close_btn.png" alt="" mode="widthFix">
        </div>
      </swiper-item>
    </swiper>

    <div class="index-title">
      云笃笃软件开发平台
    </div>
    <swiper class="banner" autoplay="true" circular="true" interval="5000" indicator-dots="true" indicator-active-color='#0699FF'>
      <swiper-item v-for="item in bannerList" :key="item.id">
        <img :src="item.href" alt="" mode="widthFix">
      </swiper-item>
    </swiper>
    <div class="business-list-box">
      <div class="business-list">
          <div class="business-item" v-for="item in businessList" :key="item.id" @click.stop="item.flag2=true">
            <div class="icon">
              <img :src="item.href" alt=""mode="widthFix">
            </div>
            <div class="title">
              {{ item.title }}
            </div>
            <!--业务电话弹窗-->
            <div class="tc-yw-box" v-show="item.flag2">
              <div class="box">
                <div class="content-box">
                  <div class="title">
                    业务电话
                  </div>
                  <div class="tel-box">
                    <div class="tel-num">
                      {{ item.tel }}
                    </div>
                    <div class="call-btn" @click.stop="callPhone(item.tel)">
                      立即拨打
                    </div>
                  </div>
                  <div class="close-btn" @click.stop="item.flag2=false">
                    <img src="/static/img/close.png" alt="" mode="widthFix">
                  </div>
                </div>
              </div>
            </div>
          </div>
      </div>
      <a href="/pages/my/main">
        <div class="my-icon">
          <img src="/static/img/my.png" alt="" mode="widthFix">
        </div>
      </a>
    </div>

  </div>
</template>

<script>
export default {
  data () {
    return {
      inforList:[],
      flag1:true,
      // flag2:false,
      bannerList:[
        {id:1,href:"/static/img/banner.jpg"}
      ],
      businessList:[
        {id:1,flag2:false,href:"/static/img/icon1.png",title:"竞价开户",tel:"15482683241"},
        {id:2,flag2:false,href:"/static/img/icon2.png",title:"公众号开发",tel:"15482683242"},
        {id:3,flag2:false,href:"/static/img/icon3.png",title:"小程序开发",tel:"15482683243"},
        {id:4,flag2:false,href:"/static/img/icon4.png",title:"各类备案",tel:"15482683244"},
        {id:5,flag2:false,href:"/static/img/icon5.png",title:"免费建站",tel:"15482683245"},
        {id:6,flag2:false,href:"/static/img/icon6.png",title:"400电话",tel:"15482683246"},
        {id:7,flag2:false,href:"/static/img/icon7.png",title:"舆情监测",tel:"15482683247"},
        {id:8,flag2:false,href:"/static/img/icon8.png",title:"非企开户",tel:"15482683248"},
        {id:9,flag2:false,href:"/static/img/icon9.png",title:"舆情监测",tel:"15482683249"},
      ],
      // tel:"15482683245"
    }
  },
  methods: {
    closeSwiper: function() {
      this.flag1=false;
    },

    callPhone: function(phone){
      wx.makePhoneCall({
        phoneNumber: phone
      })
    }
  },

  created () {

  },
  onLoad(e) {
      this.inforList=[
        { url: "url", title: "130****3452成功注册为会员" ,id:1},
        { url: "url", title: "130****3452正在咨询免费建站"  ,id:2},
        { url: "url", title: "123****5677已经提现500元"  ,id:3}];
  }
}
</script>

<style scoped>
  .index-container{
    height: 100vh;
    font-family: HiraginoSansGB-W3;
    background-color: #f8f8f8;
		box-sizing: border-box;
  }
  .swiper_container{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 50px;
    padding: 0 16px;
    background-color: #ff563f;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .swiper_container swiper-item{
    position: relative;
    display: flex;
    align-items: center;
    font-size: 16px;
    color: #fff;
  }
	.notice-icon {
		margin-right: 5px;
	}
	.notice-icon img{
		width: 20px;
		vertical-align: top;
	}
  .close-btn{
    position: absolute;
    top: 10px!important;
    right: 10px!important;
  }
  .close-btn img{
    width: 20px!important;
    vertical-align: top;
  }

  .index-title{
    height: 50px;
    line-height: 50px;
    padding: 0 17px;
    font-size: 20px;
    letter-spacing: 0px;
    color: #333333;
  }
  .banner img{
    width: 100%;
    vertical-align: top;
  }
  .business-list-box{
    margin-top:15px;
    padding: 0 15px;
    position: relative;
  }
  .business-list-box .business-list{
    display: flex;
    flex-wrap: wrap;
    background-color: #ffffff;
    box-shadow: 0 1px 5px 0
    rgba(0, 0, 0, 0.2);
    border-radius: 5px;
  }
  .business-list-box .business-list .business-item{
    flex: 0 0 33.33%;
    display: flex;
    justify-content: center;
    flex-direction: column;
    padding: 30px 0;
  }
  .business-item .icon{
    display: flex;
    justify-content: center;
  }
  .business-item .icon img{
    width: 30px;
    vertical-align: top;
  }
  .business-item .title{
    margin-top: 10px;
    text-align: center;
    font-family: HiraginoSansGB-W3;
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0;
    color: #333333;
  }
  .my-icon{
    position: absolute;
    right: 27px;
    bottom: 0;
    width: 50px;
    height: 50px;
    transform: translateY(50%);
    display: flex;
    justify-content: center;
    align-items: center;
    background-color: #ff563f;
    border-radius: 50%;
  }
  .my-icon img{
    width: 18px;
    vertical-align: middle;
  }
  /*弹窗*/
  .tc-yw-box{
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
    padding: 0 40px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .content-box{
    position: relative;
    width: 100%;
    padding: 15px 16px 20px;
    background-color: #ffffff;
    border-radius: 10px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .content-box .title{
    font-size: 18px;
    line-height: 1em;
    letter-spacing: 0;
    color: #333333;
    text-align: center;
  }
  .content-box .tel-box{
    margin-top: 50px;
  }
  .tel-box .tel-num{
    font-family: HelveticaNeueDeskInterface-Regular;
    font-size: 30px;
    line-height: 1em;
    letter-spacing: 0;
    color: #333333;
    text-align: center;
  }
  .tel-box .call-btn{
    margin: 32px 45px 0;
    height: 40px;
    line-height: 40px;
    font-size: 16px;
    letter-spacing: 0;
    color: #ffffff;
    background-color: #ff563f;
    border-radius: 20px;
    text-align: center;
  }

  .close-btn{
    position: absolute;
    right: 12px;
    top: 24px;
  }
  .close-btn img{
    width: 25px;
    vertical-align: top;
  }
</style>
