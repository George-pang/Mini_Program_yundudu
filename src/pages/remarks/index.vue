<template>
  <div class="re-container">
			<input type="text" :focus="flag" confirm-type="done" :bindconfirm="event.eventHandle" v-model.lazy="memberList[0].name" id="beizhuInput"/>
  </div>
</template>

<script>
export default {
  data () {
    return {
    	flag:true,
    	event:{
    		eventHandle: function() {
						this.flag = false;
						wx.showToast({
			        title: "备注名修改成功!",
			        icon: "none",
			        duration: 1500
			      });
			      return false;
				}
    	},
      memberList: [
        {id:1,style:"background-color: #4990fe",url:"/static/img/tx1.png",name:"繁花锦觅",tel:"12345678901",disabled:true},
        {id:2,style:"background-color: #ffb039",url:"/static/img/tx2.png",name:"淡云流水",tel:"12345678901",disabled:true},
        {id:3,style:"background-color: #f85251",url:"/static/img/tx3.png",name:"莲藕排骨",tel:"12345678901",disabled:true},
        {id:4,style:"background-color: #667ced",url:"/static/img/tx4.png",name:"木人蔷薇",tel:"12345678901", disabled: true},
			]
	}
},
	methods: {

	},

	created() {
		console.log(this.flag);
	}
}</script>

<style scoped>
  .re-container{
    height: 100vh;
    background-color: #efeff4;
    padding-top: 16px;
    box-sizing: border-box;
  }
	#beizhuInput{
		height: 44px;
		padding: 0 10px;
		font-size: 16px;
		font-weight: 500;
		background-color: #fff;
	}
</style>
