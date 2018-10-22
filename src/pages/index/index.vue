<template>
  <div id="index">
      <div class="tab1_box">
        <div class="tab1_item" v-for="(item,index) in contactLists" :key="index" @click="toCallPerson(item.phone)">
          <div class="left_zd"><img src="../../../static/images/zd.png"></div>
          <div class="right_box">
            <div class="left_number">
              <h3>{{item.phone}}</h3>
              <p>{{item.address}}{{item.type}}</p>
              <span :style="{color: item.color}">{{item.status}}</span>
              <img src="../../../static/images/star.png" v-for="(i,idx) in item.starNum" :key="idx">
            </div>
            <div class="right_time">
              <img src="../../../static/images/edit.png" @click.stop="toEditClient(item.phone)">
              <div class="time_box">
                <h5>{{item.date}} {{item.time}}</h5>
                <p>{{item.countdown}}</p>
              </div>
            </div>
          </div>
        </div>
      </div>
      <div class="fixed_bottom">
        <ul>
          <li @click="toShowClient"><img src="../../../static/images/tab1_icon1.png"></li>
          <li @click="showCall"><img src="../../../static/images/tab1_icon2.png"></li>
          <li @click="showCall"><img src="../../../static/images/tab1_icon3.png"></li>
        </ul>
      </div>
      <div class="call_layer" v-show="layerShow" @click="hideLayer"></div>
      <div class="call_box" :animation="animationCall">
        <div class="input_number" v-show="numberShow">{{number}}</div>
        <div class="number_box">
          <ul>
            <li v-for="(item,index) in numbers" :key="index" @click="writePhone(index)"><p>{{item.num}}</p><span>{{item.letter}}</span></li>
          </ul>
        </div>
        <div class="bottom_icon">
          <ul>
            <li @click="toShowClient"><img src="../../../static/images/tab1_icon1.png"></li>
            <li @click="callPhone"><div class="call_img"><img src="../../../static/images/call.png"></div></li>
            <li @click="delNumber"><img src="../../../static/images/tab1_icon3.png"></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      contactLists:[{
        id: 1,
        phone:"15814720561",
        address:"广东深圳",
        type:"移动",
        status:"意向",
        color: "#ca0505",
        starNum: 3,
        date: "10-11",
        time: "16:58",
        countdown: "58秒"
      },{
        id: 2,
        phone:"15174386509",
        address:"浙江嘉兴",
        type:"移动",
        status:"未标记",
        color: "#828282",
        starNum: 0,
        date: "10-10",
        time: "09:12",
        countdown: "3分12秒"
      },{
        id: 3,
        phone:"13689565438",
        address:"广东深圳",
        type:"移动",
        status:"无效客户",
        color: "#828282",
        starNum: 0,
        date: "10-8",
        time: "15:28",
        countdown: "2分20秒"
      },{
        id: 4,
        phone:"13689565438",
        address:"广东深圳",
        type:"移动",
        status:"初级",
        color: "#804a03",
        starNum: 1,
        date: "10-8",
        time: "15:28",
        countdown: "2分20秒"
      },{
        id: 5,
        phone:"13689565438",
        address:"广东深圳",
        type:"移动",
        status:"报价",
        color: "#009bdb",
        starNum: 0,
        date: "10-8",
        time: "15:28",
        countdown: "2分20秒"
      },{
        id: 6,
        phone:"17681546536",
        address:"浙江嘉兴",
        type:"联通",
        status:"成交",
        color: "#31ba01",
        starNum: 1,
        date: "10-8",
        time: "15:28",
        countdown: "2分20秒"
      }],
      numberShow: false,
      layerShow: false,
      animationCall: {},
      number: '',
      numbers:[{
        num:1,
        letter: ''
      },{
        num:2,
        letter: 'ABC'
      },{
        num:3,
        letter: 'DEF'
      },{
        num:4,
        letter: 'GHI'
      },{
        num:5,
        letter: 'JKL'
      },{
        num:6,
        letter: 'MNO'
      },{
        num:7,
        letter: 'PQRS'
      },{
        num:8,
        letter: 'TUV'
      },{
        num:9,
        letter: 'WXYZ'
      },{
        num:'*',
        letter: ''
      },{
        num:0,
        letter: '+'
      },{
        num:'#',
        letter: ''
      }]
    }
  },
  methods: {
    showCall(e){
      var animation = wx.createAnimation({
        transformOrigin: "50% 50%",
        duration: 300,
        timingFunction: 'ease',
        delay: 0
      })

      this.animation = animation;
      animation.bottom(0).step();
      this.layerShow = true;
      this.animationCall = animation.export();
    },
    hideLayer(e){
      var animation = wx.createAnimation({
        transformOrigin: "50% 50%",
        duration: 300,
        timingFunction: 'ease',
        delay: 0
      })

      this.animation = animation;
      animation.bottom('-100%').step();
      this.layerShow = false;
      this.animationCall = animation.export();
    },
    writePhone(index){
      this.numberShow = true;
      this.number += this.numbers[index].num
    },
    delNumber(e){
      let len = this.number.length;
      this.number = this.number.substr(0, len - 1);
      if(this.number == "" || len == 0){
        this.numberShow = false
      }
      console.log(this.number)
    },
    callPhone(e){
      if(this.number != ""){
        wx.makePhoneCall({
          phoneNumber: this.number,
          success: function(res){
            console.log(res)
          },
          fail: function(res){
            console.log(res)
          }
        })
      }else{
        wx.showToast({
          title: '请输入电话或手机号！',
          icon: 'none'
        })  
      }
    },
    toCallPerson(phone) {
      wx.makePhoneCall({
        phoneNumber: phone,
        success: function(res){
          console.log(res)
        },
        fail: function(res){
          console.log(res)
        }
      })
    },
    toEditClient(phone) {
      let url = '../edit/main?phone='+phone;
      wx.navigateTo({ url });
    },
    toShowClient(e){
      wx.reLaunch({
        url: '../client/main',
      })
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
    }
  }
}
</script>

<style scoped>
  .number_box{
    overflow: hidden;
    padding: 15px 15px 0;
    border-top: 1px solid #EAEAEA;
  }
  .input_number{
    height: 40px;
    line-height: 40px;
    background: #fff;
    text-align: center;
    color: #171717;
    font-size: 22px;
    border-top: 1px solid #EAEAEA;
  }
  .number_box ul{
    overflow: hidden;
    display: flex;
    align-items: top;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  .number_box ul li{
    width: 30%;
    text-align: center;
    margin-bottom: 15px;
    overflow: hidden;
  }
  .number_box ul li p{
    color: #171717;
    font-size: 30px;
  }
  .number_box ul li span{
    display: block;
    color: #171717;
    font-size: 11px;
  }
  .call_box{
    background: #fff;
    position: fixed;
    width: 100%;
    left: 0;
    bottom: -100%;
    z-index: 10;
  }
  .call_layer{
    width: 100%;
    height: 100%;
    position: fixed;
    left: 0;
    top: 0;
    z-index: 8;
  }

  .tab1_box{
    overflow: hidden;
    padding: 5px 15px 50px;
  }
  .tab1_item{
    margin-top: 25px;
    overflow: hidden;
  }
  .left_zd{
    width: 10%;
    float: left;
  }
  .left_zd img{
    display: block;
    width: 12px;
    height: 12px;
    margin-top: 5px;
  }
  .right_box{
    width: 90%;
    float: right;
    border-bottom: 1px solid #E7E7E7;
    overflow: hidden;
    padding-bottom: 15px;
  }
  .tab1_item:last-child .right_box{
    border-bottom: 0;
  }
  .left_number{
    width: 50%;
    float: left;
  }
  .left_number h3{
    color: #282828;
    font-size: 16px;
    margin-bottom: 5px;
  }
  .left_number p{
    color: #828282;
    font-size: 13px;
  }
  .left_number span{
    /*color: #ca0505;*/
    font-size: 13px;
    margin: 0 7px 0 0;
    vertical-align: middle;
  }
  .left_number img{
    display: inline-block;
    vertical-align: middle;
    width: 14.5px;
    height: 13.5px;
    margin-right: 3px;
  }
  .right_time{
    width: 50%;
    float: right;
    overflow: hidden;
  }
  .time_box{
    float: right;
    text-align: right;
  }
  .time_box h5{
    margin-bottom: 5px;
  }
  .time_box h5,.time_box p{
    color: #717171;
    font-size: 13px;
  }
  .right_time img{
    display: block;
    float: right;
    width: 25.5px;
    height: 21.5px;
    margin: 4px 0 0 15px;
  }

  .fixed_bottom{
    width: 100%;
    overflow: hidden;
    position: fixed;
    left: 0;
    bottom: 0;
    background: #fff;
    border-top: 1px solid #F1F1F1;
    z-index: 5;
  }
  .fixed_bottom ul{
    overflow: hidden;
  }
  .fixed_bottom ul li,.bottom_icon ul li{
    width: 33.3%;
    height: 50px;
    float: left;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .bottom_icon ul li{
    height: 70px;
  }
  .fixed_bottom ul li img,.bottom_icon ul li img{
    display: inline-block;
    width: 25px;
    height: 26.5px;
  }
  .bottom_icon ul li .call_img{
    width: 52.5px;
    height: 52.5px;
    border-radius: 50%;
    background: #51cb79;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .bottom_icon ul li .call_img img{
    width: 24.5px;
    height: 24.5px;
  }
</style>