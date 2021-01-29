<template>
    <div>
    <div class="modal-mask"></div>
      <div class="modal-dialog">
        <div class="modal-content">
          <img class="modal-img" src="../../static/images/littleTip.png">
          <div class="content-text">
            <p class="key-bold">体检宝是以公益性为目的，</p>
            <p class="key-bold">为中小学生量身定制的健康管理小程序。</p>
            <p class="little-content">通过纵向分析实时数据与学校体检数据，提出健康建议，有效干预和管理中小学生健康。</p>
          </div>
        </div>
        <div class="modal-footer">
          <button open-type="getUserInfo" lang="zh_CN" class="btn" @getuserinfo="login">
            授权登录</button>
        </div>
      </div>
    </div>
</template>

<script>
import config from '@/config'
import qcloud from 'wafer2-client-sdk'
import util from '@/utils/util.js'
export default{
  methods: {
    login () {
      qcloud.setLoginUrl(config.loginUrl)
      qcloud.login({
        success: userInfo => {
          console.log('登录成功', userInfo)
          this.loginSuccess(userInfo)
          this.$emit('changeShow', false, userInfo)
          wx.showTabBar()
          util.showSuccess('登录成功')
        },
        fail: err => {
          console.log('登录失败', err)
        }
      })
    },
    loginSuccess (userInfo) {
      wx.setStorageSync('userinfo', userInfo)
    }
  }
}
</script>

<style lang="scss">
.modal-mask {
  width: 100%;
  height: 100%;
  position: fixed;
  top: 0;
  left: 0;
  background: #000;
  opacity: 0.5;
  overflow: hidden;
  z-index: 9000;
  color: #fff;
}
.modal-dialog {
  box-sizing: border-box;
  width: 560rpx;
  overflow: hidden;
  position: fixed;
  top: 30%;
  left: 0;
  z-index: 9999;
  background: #fff;
  margin: -150rpx 95rpx;
  border-radius: 16rpx;
}
.modal-content {
  box-sizing: border-box;
  display: flex;
  padding: 0rpx 53rpx 50rpx 53rpx;
  font-size: 32rpx;
  align-items: center;
  justify-content: center;
  flex-direction: column;
}
.content-tip {
  text-align: center;
  font-size: 36rpx;
  color: #333333;
}
.content-text {
  height:260rpx;
  padding:20rpx 0rpx 100rpx 0rpx;
  font-size:28rpx;
}
.modal-footer {
  box-sizing: border-box;
  display: flex;
  flex-direction: row;
  border-top: 2rpx solid #e5e5e5;
  font-size: 32rpx;
  font-weight:bold;
  height: 90rpx;
  line-height: 90rpx;
  text-align: center;
  background:#1EDE8F;
}
button {
  width: 100%;
  background:#1EDE8F;
  color:#FFFFFF;
  font-weight:bold;
}
.modal-img {
  width: 569rpx;
  height:180rpx;
}
.little-content {
  padding-top:30rpx;
  font-size: 28rpx;
  color:#606060;
}
.key-bold {
  padding-top:10rpx;
  font-size: 28rpx;
  font-weight:bold;
}
</style>