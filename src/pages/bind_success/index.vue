<template>
  <div class="bind-container">
      <div class="bg">
          <div class="bind_suc">
            <div class="icon">
              <img src="/static/img/ok.png" alt="" mode="widthFix">
            </div>
            <div class="tips">
              绑定成功
            </div>
          </div>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {

    }
  },
  methods: {

  },

  onLoad: function() {
  var timeId=setTimeout(function(){
      wx.redirectTo({
        url: '/pages/integral/main'
      });
    clearTimeout(timeId);
    },2000)
  }

}
</script>

<style scoped>
  .bind-container{
    position: relative;
    height: 100vh;
    font-family: HiraginoSansGB-W3;
    background-color: #f8f8f8;
  }
  .bg{
    position: relative;
    height: 285rpx;
    background-color: #ff563f;
  }
  .bind_suc{
    position: absolute;
    top: 25px;
    left: 50%;
    transform: translateX(-50%);
  }
  .bind_suc .icon img{
    width: 55px;
    vertical-align: top;
  }
  .bind_suc .tips{
    margin-top: 15px;
    font-size: 16px;
    line-height: 1em;
    letter-spacing: 0px;
    color: #ffffff;
  }

</style>
