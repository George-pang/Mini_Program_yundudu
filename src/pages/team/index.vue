<template>
  <div class="team-container">
      <div class="member-list">
          <div class="list-item" v-for="item in memberList" :key="item.id">
              <div class="item-left">
                <div class="l-line" :style="item.style"></div>
                <div class="user-avatar">
                  <img :src="item.url" alt="" mode="widthFix">
                </div>
                <div class="user-info">
                  <input type="text" v-model="item.name" :disabled="item.disabled" id="user-name" >
                  <input type="tel" v-model="item.tel" class="user-tel" disabled>
                </div>
              </div>
              <div class="item-right remarks" @click="clickHandle()">
                  <div class="icon">
                    <img src="/static/img/beizhu.png" alt="" mode="widthFix">
                  </div>
                  <div class="text">
                	    备注
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
      memberList: [
        {id:1,style:"background-color: #4990fe",url:"/static/img/tx1.png",name:"繁花锦觅",tel:"12345678901",disabled:true},
        {id:2,style:"background-color: #ffb039",url:"/static/img/tx2.png",name:"淡云流水",tel:"12345678901",disabled:true},
        {id:3,style:"background-color: #f85251",url:"/static/img/tx3.png",name:"莲藕排骨",tel:"12345678901",disabled:true},
        {id:4,style:"background-color: #667ced",url:"/static/img/tx4.png",name:"木人蔷薇",tel:"12345678901",disabled:true},
      ]
    }
  },
  methods: {
    clickHandle: function() {
    wx.navigateTo({
    	url:"/pages/remarks/main",
    })
    }
  },

  created () {

  }
}
</script>

<style scoped>
  .team-container{
    height: 100vh;
    background-color: #f8f8f8;
  }
  .member-list{
    padding: 15px 16px;
  }
  .list-item{
    height: 100px;
    margin-top: 15px;
    background-color: #ffffff;
    box-shadow: 0 1px 7px 0
    rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    overflow: hidden;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .list-item:nth-child(1){
    margin-top: 0;
  }
  .item-left{
    display: flex;
    align-items: center;
    height: 100%;
  }
  .item-left .l-line{
    width: 7px;
    height: 100%;
  }
  .item-left .user-avatar{
    display: flex;
    align-items: center;
    margin-left: 7px;
    margin-right: 10px;
  }
  .item-left .user-avatar img{
    width: 70px;
    vertical-align: middle;
  }
  .item-left .user-info{
    /*display: flex;*/
    /*flex-direction: column;*/
    /*align-items: center;*/
  }
  .user-info #user-name{
    font-size: 16px;
    height: 20px;
    line-height: 20px;
    min-height: 20px;
    letter-spacing: 0px;
    color: #333333;
  }
  .user-info .user-tel{
    margin-top: 10px;
    font-family: HelveticaNeueDeskInterface-Regular;
    font-size: 14px;
    height: 20px;
    line-height: 20px;
    min-height: 20px;
    letter-spacing: 0;
    color: #999999;
  }
  .item-right{
    display: flex;
    align-items: center;
    padding: 0 16px;
  }
  .item-right .icon{
    display: flex;
    align-items: center;
  }
  .icon img{
    width: 14px;
    vertical-align: top;
  }
  .item-right .text{
    margin-left: 5px;
    font-size: 14px;
    line-height: 1em;
    letter-spacing: 0;
    color: #999999;
    white-space: nowrap;
  }
  .tc-remarks{
  	position: fixed;
  	
  }
</style>
