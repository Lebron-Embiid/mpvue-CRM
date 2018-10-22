<script>
export default {
  created () {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)

    console.log('app created and cache logs by setStorageSync')
  }
}
</script>

<style>
.container {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 200rpx 0;
  box-sizing: border-box;
}
/* this rule will be remove */
* {
  transition: width 2s;
  -moz-transition: width 2s;
  -webkit-transition: width 2s;
  -o-transition: width 2s;
}
button::after{
  border: 0;
}

.call_layer,.filter_wrapper,.time_wrapper{
  width: 100%;
  height: 100%;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 8;
}


.release{
  position: fixed;
  right: 15px;
  bottom: 15px;
  z-index: 10;
}
.release a{
  background: #009bdb;
  width: 53px;
  height: 53px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.release a img{
  display: block;
  width: 23.5px;
  height: 23.5px;
}


.edit_header{
  position: fixed;
  width: 100%;
  height: 48px;
  top: 0;
  left: 0;
  background: #eee;
  z-index: 6;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.edit_header .back,
.edit_header .save{
  color: #109dd8;
  font-size: 14px;
  width: 15%;
  text-align: center;
}
.header_title{
  color: #1f1f1f;
  font-size: 15px;
}


.edit_box{
  padding-bottom: 5px;
  border-bottom: 1px solid #ECECEC;
}
.edit_box h3{
  color: #000;
  font-size: 13px;
  margin: 15px 0 10px;
}
.edit_box ul{
  overflow: hidden;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.edit_box ul li{
  width: 22%;
  height: 35px;
  display: flex;
  justify-content: center;
  align-items: center;
  border: 1px solid #E7E7E7;
  background: #fcfcfc;
  color: #6a6a6a;
  font-size: 13px;
  margin-bottom: 10px;
}
.edit_box ul li.active{
  color: #109dd8;
  border-color: #109dd8;
}
.edit_box textarea{
  background: #fcfcfc;
  display: block;
  width: 100%;
  height: 115px;
  border: 1px solid #E6E6E6;
  color: #a6a6a6;
  font-size: 12px;
  padding: 10px 15px;
  box-sizing: border-box;
  margin-bottom: 20px;
  outline: none;
  resize: none;
}
</style>
