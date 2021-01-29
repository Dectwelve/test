<template>
  <div class="indexcolor">
  	<!-- 登录组件 -->
  	<div v-if="showLogin">
      <LoginWindow @changeShow = "getModel(arguments)"></LoginWindow>
    </div>
    <div class="health" v-if="state===1">
      <label class="atext">健康状态</label>
      <label class="btext">健康</label>
    </div>
    <div class="subhealth" v-if="state===2">
      <label class="atext">健康状态</label>
      <label class="btext">亚健康</label>
    </div>
    <div class="disease" v-if="state===3">
      <label class="atext">健康状态</label>
      <label class="btext">疾病</label>
    </div>
    <div class="bigbox">
	    <!-- 体检中心 -->
	    <div class="indexbox">
	    	<div class="functiontitle">体检中心</div>
	    	<div class="functionbox">
	    		<div class="function" @click="onData">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/data.png"></van-image>
	    			<label class="ctext">体检数据</label>
	  			</div>
	  			<div class="function" @click="onAnalyse">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/analyse.png"></van-image>
	    			<label class="ctext">报告分析</label>
	  			</div>
	  			<div class="function" @click="onSuggest">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/suggest.png"></van-image>
	    			<label class="ctext">健康建议</label>
	  			</div>
	    	</div>
	    </div>
	    <!-- 实用工具 -->
	    <div class="indexbox">
	    	<div class="functiontitle">实用工具</div>
	    	<div class="functionbox">
	    		<div class="function" @click="onIndex">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/index.png"></van-image>
	    			<label class="ctext">健康指数</label>
	  			</div>
	  			<div class="function" @click="onPevent">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/prevent.png"></van-image>
	    			<label class="ctext">防控</label>
	  			</div>
	  			<div class="function" @click="onGarden">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/garden.png"></van-image>
	    			<label class="ctext">健康园地</label>
	  			</div>
	    	</div>
	    </div>
	    <!-- 商务定制 -->
	    <div class="indexbox">
	    	<div class="functiontitle">商务定制</div>
	    	<div class="functionbox">
	    		<div class="function" @click="onExercise">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/exercise.png"></van-image>
	    			<label class="ctext">健康锻炼</label>
	  			</div>
	  			<div class="function" @click="onDiet">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/diet.png"></van-image>
	    			<label class="ctext">饮食搭配</label>
	  			</div>
	  			<div class="function" @click="onDevices">
	    			<van-image width="80rpx" height="80rpx" src="../../../static/images/devices.png"></van-image>
	    			<label class="ctext">穿戴设备</label>
	  			</div>
	    	</div>
	    </div>
	</div>
  </div>
</template>

<script>
import util from '@/utils/util.js'
import LoginWindow from '@/components/LoginWindow'
export default {
  components: {
  	LoginWindow
  },
  data () {
  	return {
  		state: 1,
  		showLogin: false
  	}
  },
  methods: {
  	getModel (val) {
  		this.show = true
  		this.showLogin = val[0]
  		this.userinfo = val[1]
  		// this.getCurrentMark()
  	},
  	onData () {
  		// wx.showActionSheet({
  		// 	itemList: ['A', 'B', 'C'],
  		// 	success (res) {
  		// 		console.log(res.tapIndex)
  		// 	},
  		// 	fail (res) {
  		// 		console.log(res.errMsg)
  		// 	}
  		// })
  		wx.navigateTo({
  		  url: '/pages/data/main'
  		})
  	},
  	onAnalyse () {
  		util.showModal('提示', '该功能尚未开发')
  	},
  	onSuggest () {
  		util.showModal('提示', '该功能尚未开发')
  	},
  	onIndex () {
  		util.showModal('提示', '该功能尚未开发')
  	},
  	onPevent () {
  		util.showModal('提示', '该功能尚未开发')
  	},
  	onGarden () {
  		util.showModal('提示', '该功能尚未开发')
  	},
  	onExercise () {
  		util.showModal('提示', '该功能尚未开发')
  		this.state = 2
  		wx.setNavigationBarColor({
  			frontColor: '#ffffff',
  			backgroundColor: '#FBDB05',
  			animation: {
  				duration: 0,
  				timingFunc: 'linear'
  			}
  		})
  	},
  	onDiet () {
  		util.showModal('提示', '该功能尚未开发')
  		this.state = 3
  		wx.setNavigationBarColor({
  			frontColor: '#ffffff',
  			backgroundColor: '#F78D7E',
  			animation: {
  				duration: 0,
  				timingFunc: 'linear'
  			}
  		})
  	},
  	onDevices () {
  		util.showModal('提示', '该功能尚未开发')
  		this.state = 1
  		wx.setNavigationBarColor({
  			frontColor: '#ffffff',
  			backgroundColor: '#1EDE8F',
  			animation: {
  				duration: 0,
  				timingFunc: 'linear'
  			}
  		})
  	}
  },
  mounted () {
  	const userinfo = wx.getStorageSync('userinfo')
  	if (userinfo.openId) {
  		this.userinfo = userinfo
  		console.log('用户信息：', this.userinfo)
  	} else {
  		wx.hideTabBar()
  		this.showLogin = true
  	}
  }
}
</script>

<style lang="scss">
page{
	height: 100%;
}
.indexcolor{
	height: 100%;
	width: 100%;
	background-color: #EDF4F4;
	.health{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: #1EDE8F;
		height: 25%;
		.atext{
			color: #fff;
			margin-bottom: 20rpx;
		}
		.btext{
			color: #fff;
			font-size: 66rpx;
			font-weight: bold;
		}
	}
	.subhealth{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: #FBDB05;
		height: 25%;
		.atext{
			color: #fff;
			margin-bottom: 20rpx;
		}
		.btext{
			color: #fff;
			font-size: 66rpx;
			font-weight: bold;
		}
	}
	.disease{
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		background-color: #F78D7E;
		height: 25%;
		.atext{
			color: #fff;
			margin-bottom: 20rpx;
		}
		.btext{
			color: #fff;
			font-size: 66rpx;
			font-weight: bold;
		}
	}
	.bigbox{
		display: flex;
		flex-direction: column;
		height: 75%;
		.functiontitle{
			font-size: 34rpx;
			font-weight: 600;
			padding: 15rpx 20rpx;
		}
		.indexbox{
			margin: 30rpx 20rpx 0rpx;
			background-color: #fff;
			border-radius: 20rpx;
			height:28%;
			.functionbox{
				display: flex;
				flex-direction: row;
				justify-content: space-around;
				.function{
					justify-content: center;
					align-items: center;
					display: flex;
					flex-direction: column;
				}
			}
		}
	}
}

</style>
