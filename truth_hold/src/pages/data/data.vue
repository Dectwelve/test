<template>
  <div>
    <div class="dateselect">
      <van-icon name="../../../static/images/calendar.png"/>
      <div class="picker">
        <picker
          style="position: absolute;text-align: left;width: 100%" 
          mode="date" 
          :value="date" 
          @change="dateChange">{{date}}
        </picker>
      </div>
      <div class="downimg">
        <van-icon  name="../../../static/images/down.png"/>
      </div>
    </div>
    <van-cell-group>
      <van-cell
        custom-class="databox"
        icon="../../../static/images/calendar.png"
        is-link
        arrow-direction="down"
        :title="date"
        @click="inName"
      ></van-cell>
    </van-cell-group>
  </div>
</template>

<script>
export default {
  data () {
  	return {
  		date: '2021-1-28'
  	}
  }
}
</script>

<style lang="scss">
page{
  background-color: #EDF4F4;
}
.databox{
  margin-top: 20rpx;
  border-radius: 5%;
}
.dateselect{
  display: flex;
  flex-direction: row;
  padding: 0px 35rpx;
  margin: 20rpx 30rpx;
  height: 90rpx;
  background-color: #fff;
  line-height: 90rpx;
  .picker{
    margin-left:20rpx;
  }
  .downimg{
    margin: 4rpx 180rpx;
  }
}
</style>
