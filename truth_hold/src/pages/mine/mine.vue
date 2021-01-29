<template>
  <div>
  	<div class="top">
	    <!-- 头像 -->
      <div class="userinfo">
        <img :src="face">
      </div>
      <div class="name">
        <!-- 姓名 -->
        <label>{{name}}</label>
        <!-- 更换头像 -->
        <div class="show-maxim" @click="uploadPicture">点击更换头像</div>
      </div>
    </div>
    <van-cell-group>
      <van-cell
        custom-class="kong"
        icon="../../../static/images/name.png"
        is-link
        title="姓名"
        @click="inName"
      ></van-cell>
      <van-cell
        custom-class="kong"
        icon="../../../static/images/school.png"
        is-link
        title="学校"
        @click="inSchool"
      ></van-cell>
      <van-cell
        custom-class="kong"
        icon="../../../static/images/grade.png"
        is-link
        title="年级"
        @click="inGrade"
      ></van-cell>
      <van-cell
        custom-class="kong"
        icon="../../../static/images/gender.png"
        is-link
        title="性别"
        @click="inGender"
      ></van-cell>
      <van-cell
        custom-class="kong"
        icon="../../../static/images/birth.png"
        is-link
        title="生日"
        @click="inBirth"
      ></van-cell>
      <van-cell
        custom-class="space"
        icon="../../../static/images/question.png"
        is-link
        title="关于我们"
        link-type="navigateTo"
        url="/pages/aboutour/main"
      ></van-cell>
    </van-cell-group>
    <!-- 弹窗 -->
    <div>
      <van-dialog
        use-slot
        :title="title"
        :show="show"
        show-cancel-button
        @close="onClose"
        @confirm="onConfirm"
      >
        <van-field
          :value="changecontent"
          :placeholder="placeholder"
          border="false"
          @change="onChange"
        />
      </van-dialog>
    </div>
  </div>
</template>

<script>
// import util from '@/utils/util.js'
export default{
  data () {
  	return {
  		userinfo: {},
  		face: '',
  		name: '姓名',
      school: 'xue',
      birth: '22-22-22',
      grade: '二年级',
      gender: '女',
      title: '',
      show: false,
      changecontent: '',
      state: 0,
      placeholder: ''
  	}
  },
  methods: {
    // 更换头像
    uploadPicture () {
      // 将this保存到that上面
      const that = this
      wx.chooseImage({
        count: 1,
        sizeType: ['original', 'compressed'],
        sourceType: ['album', 'camera'],
        success (res) {
          // tempFilePath可以作为img标签的src属性显示图片,即上传的图片数据
          const tempFilePaths = res.tempFilePaths
          // 用that.src来调用data函数定义的src变量
          that.face = tempFilePaths
          console.log('图片路径', that.face)
        }
      })
    },
    onClose () {
      this.show = false
    },
    onConfirm () {
      switch (this.state) {
        case 1:
          this.name = this.changecontent
          break
        case 2:
          this.school = this.changecontent
          break
        case 3:
          this.grade = this.changecontent
          break
        case 4:
          this.gender = this.changecontent
          break
        case 5:
          this.birth = this.changecontent
          break
      }
    },
    // 显示弹窗
    inName () {
      this.show = true
      this.state = 1
      this.title = '姓名'
      this.placeholder = '请填写姓名'
      // 从后端获取信息代码，让this.changecontent=信息getInformation(this.state)
      this.changecontent = this.name
    },
    inSchool () {
      this.show = true
      this.state = 2
      this.title = '学校'
      this.placeholder = '请填写校名'
      this.changecontent = this.school
      // 从后端获取信息代码，让this.changecontent=信息getInformation(this.state)
    },
    inGrade () {
      this.show = true
      this.state = 3
      this.title = '年级'
      this.placeholder = '格式：一年级 / 初一 / 高一'
      // 从后端获取信息代码，让this.changecontent=信息getInformation(this.state)
    },
    inGender () {
      this.show = true
      this.state = 4
      this.title = '性别'
      this.placeholder = '女 / 男'
      // 从后端获取信息代码，让this.changecontent=信息getInformation(this.state)
    },
    inBirth () {
      this.show = true
      this.state = 5
      this.title = '生日'
      this.placeholder = '格式：XXXX-XX-XX'
      // 从后端获取信息代码，让this.changecontent=信息getInformation(this.state)
    },
    // 编辑内容
    onChange (event) {
      this.changecontent = event.mp.detail
    }
  },
  mounted () {
  	const userinfo = wx.getStorageSync('userinfo')
  	this.face = userinfo.avatarUrl
  }
}
</script>

<style lang="scss">
page{
  background-color: #EDF4F4;
}
.top{
  background:#62ceff;
  border-radius: 20rpx;
  margin: 20rpx;
  display: flex;
  .userinfo{
    margin: 30rpx;
    float: left;
    img{
      width: 140rpx;
      height: 140rpx;
      border-radius: 20%;
      border: 4rpx #ffffff solid;
    }
  }
  .name{
    margin: 30rpx 0rpx;
    color: #FFFFFF;
    font-size: 50rpx;
    display: flex;
    flex-direction: column; 
    justify-content: space-around;
    .show-maxim{
      font-size: 28rpx;
    }
  }
}
.kong{
  margin-top: 4rpx;
  border-radius: 5%;
}
.space{
  margin-top: 26rpx;
}
</style>