<template>
  <div class="my-container">
    <div class="userinfo-box">
      <img src="/static/img/mybg.jpg" alt="" mode="widthFix">
			<!--获取微信头像和昵称--源自初始化项目中的代码-->
      <div class="userinfo" @click="bindViewTap">
        <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
        <div class="userinfo-nickname">
          <card :text="userInfo.nickName"></card>
        </div>
      </div>
    </div>
    <div class="my-list">
        <div class="list-item" v-for="item in mylist" :key="item.id">
          <a :href="item.href">
            <div class="item">
                <div class="item-left">
                  <div class="icon">
                    <img :src="item.url" alt="" mode="widthFix">
                  </div>
                  <div class="title">
                    {{ item.title }}
                  </div>
                </div>
                <div class="item-right">
                    <div class="add-info">
                      {{ item.info }}
                    </div>
                    <div class="icon-more">
                      <img src="/static/img/more.png" alt="" mode="widthFix">
                    </div>
                </div>
            </div>
          </a>
        </div>
    </div>
  </div>
</template>

<script>

import card from '@/components/card'

export default {
  data () {
    return {
      userInfo: {},
      mylist: [
        {id:1,href:"/pages/qrcode/main",url:"/static/img/erweima.png",title:"我的二维码",info:""},
        {id:2,href:"/pages/integral/main",url:"/static/img/jifen.png",title:"我的积分",info:"2300分"},
        {id:3,href:"/pages/team/main",url:"/static/img/team.png",title:"我的团队",info:""}
      ]
    }
  },
  components: {
    card
  },
  methods: {
    //查看启动日志
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  },
}
</script>

<style scoped>
  .my-container{
    height: 100vh;
    background-color: #f8f8f8;
  }
  .userinfo-box{
    position: relative;
    overflow: hidden;
  }
  .userinfo-box >img{
    width: 100%;
    vertical-align: top;
  }
  .userinfo {
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .userinfo-avatar {
    width: 80px;
    height: 80px;
    margin: 13px;
    border-radius: 50%;
  }

  .userinfo-nickname {
    margin-top: 6px;
    font-size: 18px;
    letter-spacing: 0;
    color: #fff;
  }

  .my-list{
    margin-top: 27px;
    padding: 0 16px;

  }
  .my-list .list-item{
    margin-top: 35px;
    height: 20px;
  }
  .my-list .list-item:nth-child(1){
    margin-top: 0;
  }
  .my-list .list-item a{
    display: block;
    height: 100%;
  }
  .my-list .list-item .item{
    display: flex;
    justify-content: space-between;
    height: 100%;
  }
  .item .item-left,.item .item-right{
    display: flex;
    align-items: center;
  }
  .item-left .icon{
    display: flex;
    align-items: center;
  }
  .item-left .icon img{
    width: 16px;
    vertical-align: top;
  }
  .item-left .title{
    margin-left: 10px;
    font-family: HiraginoSansGB-W3;
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0;
    color: #333333;
  }
  .item-right .add-info{
    font-family: HiraginoSansGB-W3;
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0;
    color: #999999;
    margin-right: 10px;
  }
  .item-right .icon-more{
    display: flex;
    align-items: center;
  }
  .item-right .icon-more img{
    width: 15px;
    vertical-align: top;
  }

</style>
