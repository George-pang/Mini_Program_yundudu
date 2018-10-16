<template>
  <div class="integral-container">
		<div class="my-integral">
      <img src="/static/img/integ_bg.png" alt="" mode="widthFix">
		   <div class="integral-row">
		   		<div class="integral">
		   				{{ integral }}积分
		   		</div>
         <a href="/pages/card/main">
            <div class="bind-card">
                绑定银行卡
            </div>
         </a>
		   </div>
		</div>
		<div class="nav-hd">
			<div class="nav-item" v-for="(item,index) in tabs" :key="item.id" :class="{active:index == num2}" @click="tab(index)">
          <div class="item-title" :style="item.style">{{ item.title }}</div>
          <!--<div class="item-line"  v-show="item.flag"></div>-->
      </div>
		</div>
    <div class="nav-bd">
      <div class="bd-item" v-for="(item,index) in tabContents" :key="item.id" v-show="index == num2">
        <div class="bd-inner-box">
            <div class="item input-item">
              <div class="item-title">
                提现积分
              </div>
              <div class="item-num">
                <input type="number" placeholder="请输入要提现的积分数额" v-model="num">
                <span>分</span>
              </div>
            </div>
            <div class="item input-item">
              <div class="item-title">
                到账金额
              </div>
              <div class="item-num">
                <!--<input type="number" v-model.number="parseInt(num)/10" disabled>-->
                <input type="number" :value="num/10" disabled>
                <span>元</span>
              </div>
            </div>
            <div class="item confirm-item">
              <div class="item-title">
                <div class="tips" v-if="item.flag2">
                  <img src="/static/img/wrong.png" alt="" mode="widthFix">
                  <span>请绑定银行卡</span>
                </div>
              </div>
              <div class="item-num">
                  <div class="confirm-btn" @click="submit">
                      确认
                  </div>
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
      // num:parseInt(""),
      integral:2300,
      num:"",
      flag:true,
      tabs: [
        {id:1,title:"提现到微信"},
        {id:2,title:"提现到银行卡"}
      ],
      tabContents:[
        {id:1,flag2:false},
        {id:2,flag2:true},
      ],
      num2:0
    }
  },
  methods: {
    tab(index) {
      this.num2 = index;
      console.log(typeof this.num);
      // this.num=parseInt("");
      this.num="";
    },
    submit: function() {
      if (this.num==""){
        wx.showToast({
          title: "请输入要提现的积分数额！", //提示的内容
          icon: "none",
          duration: 1500
        });
        return false;
      }else if (parseInt(this.num)>this.integral) {
        wx.showToast({
          title: "您的可供提现积分不足！", //提示的内容
          icon: "none",
          duration: 1500
        });
        return false;
      }else{
        wx.showToast({
          title: "积分提现申请已发起,请耐心等待到账！", //提示的内容
          icon: "none",
          duration: 1500
        });
        return false;
      }
    }
  },

  created () {

  }
}
</script>

<style scoped>
  .integral-container{
      height: 100vh;
      background-color: #f8f8f8;
  }
  .my-integral{
  	position: relative;
  	height: 106px;
  	/*background-color: #ff563f;*/
  }
  .my-integral img {
    width: 100%;
    vertical-align: top;
  }
  .integral-row{
  	position: absolute;
  	top: 23px;
  	left: 0;
  	width: 100%;
  	padding: 0 16px 0 31px;
  	box-sizing: border-box;
  	display: flex;
  	justify-content: space-between;
  }
  .integral-row .integral{
  	font-family: HelveticaNeueDeskInterface-Regular,HiraginoSansGB-W3;
  	font-size: 24px;
  	height: 30px;
  	line-height: 30px;
  	letter-spacing: 0px;
  	color: #ffffff;
  }
  .integral-row .bind-card{
  	height: 30px;
  	padding: 0 10px;
  	font-size: 14px;
  	line-height: 28px;
  	letter-spacing: 0px;
  	color: #ffffff;
  	border-radius: 15px;
  	border: solid 1px #ffffff;
  	box-sizing: border-box;
  }
  .nav-hd{
  	height: 35px;
  	display: flex;
  	background-color: #ffffff;
  	box-shadow: 0px 1px 3px 0px
  		rgba(0, 0, 0, 0.1);
  }
  .nav-hd .nav-item{
    position: relative;
  	flex: 1;
  }
  .nav-item .item-title{
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 14px;
    letter-spacing: 0px;
    color: #666;
    /*color: #ff563f;*/
  }

  .active .item-title{
    color: #ff563f;
  }
  .active::after{
    content: '';
    position: absolute;
    bottom: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 100px;
    height: 2px;
    background-color: #ff563f;
  }
  .nav-bd{
    margin-top: 25px;
    position: relative;
  }
  .nav-bd .bd-item{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    padding: 0 16px;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
  }
  .bd-inner-box{
    padding: 0 10px;
    background-color: #ffffff;
    box-shadow: 0px 1px 5px 0px
    rgba(0, 0, 0, 0.15);
    border-radius: 5px;
  }
  .bd-inner-box .item{
    height: 50px;
    display: flex;
    min-width: 0;
    justify-content: space-between;
    align-items: center;
  }
  .item .item-title{
    width: 80px;
    margin-right: 10px;
    font-size: 16px;
    letter-spacing: 0px;
    color: #333333;
    overflow: hidden;
    text-overflow: ellipsis;
    white-space: nowrap;
  }
  .item .item-num{
    flex: 1;
    min-width: 0;
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }
  .item .item-num>input{
    flex: 1;
    padding: 0 10px;
    text-align: right;
    font-size: 12px;
    letter-spacing: 0px;
    color: #999999;
  }
  .item .item-num>span{
    font-size: 16px;
    letter-spacing: 0px;
    color: #333333;
  }
  .item:nth-child(2) .item-num>input{
    font-size: 16px;;
    letter-spacing: 0px;
    color: #ff563f;
  }
  .input-item{
    position: relative;
  }
  .input-item::after{
    content: "";
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 1px;
    background-color: #eeeeee;
  }
  .confirm-item .item-title .tips{
    display: flex;
    align-items: center;
  }
  .tips img{
    width: 15px;
    margin-right: 5px;
  }
  .tips span{
    font-size: 12px;
    letter-spacing: 0px;
    color: #ff5959;
  }
  .confirm-item .confirm-btn{
    height: 31px;
    padding: 0 30px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0px;
    color: #feffff;
    background-color: #ff563f;
    border-radius: 15px;
  }
</style>
