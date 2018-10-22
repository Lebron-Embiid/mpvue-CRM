<template>
	<div id="remindAdd">
		<div class="edit_header">
			<div class="back" @click="cancleBack">取消</div>
			<div class="header_title">{{title}}</div>
			<div class="save" @click="saveBack">保存</div>
		</div>
		<div class="remindAdd_box">
			<div class="edit_box">
				<h3>提醒时间</h3>
				<div class="time_box" @click="selectTime">
					<span>{{month}}月{{day}}日</span><span>{{week}}</span><span>{{hour}}:{{minute}}</span>
					<img src="../../../static/images/edit_remind.png">
				</div>
				
				<div class="time_wrapper" v-show="timeShow" @click="hideTime"></div>
				<div class="time_layer" :animation="animationTime">
					<div class="time_top">
						<div class="t_left" @click="hideTime">取消</div>
						<h2>请选择提醒时间</h2>
						<div class="t_right" @click="queryTime">确定</div>
					</div>
					<picker-view indicator-style="height: 50px;" style="width: 100%; height: 200px;" :value="value" @change="bindChange">
						<picker-view-column>
							<view v-for="(item,index) in years" :key="index" style="line-height: 50px">{{item}}年</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in months" :key="index" style="line-height: 50px">{{item}}月</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in days" :key="index" style="line-height: 50px">{{item}}日</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in hours" :key="index" style="line-height: 50px">{{item}}时</view>
						</picker-view-column>
						<picker-view-column>
							<view v-for="(item,index) in minutes" :key="index" style="line-height: 50px">{{item}}分</view>
						</picker-view-column>
					</picker-view>
				</div>
				<!-- <ul>
					<li v-for="(item,index) in timeLabels" :key="index" @click="selectTime(index)" :class="item.status == true?'active':''">{{item.title}}</li>
				</ul> -->
			</div>
			<div class="edit_box">
				<h3>提醒内容</h3>
				<textarea name="content" placeholder="请输入提醒内容"></textarea>
			</div>
		</div>
	</div>
</template>

<script>
const date = new Date()
const years = []
const months = []
const days = []
const hours = []
const minutes = []
let timeIdx = []
for (let i = date.getFullYear(); i <= date.getFullYear()+2; i++) {
  years.push(i)
}

for (let i = 1 ; i <= 12; i++) {
	if(i<10){
		i = "0"+i
	}
  months.push(i)
}

for (let i = 1 ; i <= 31; i++) {
	if(i<10){
		i = "0"+i
	}
  days.push(i)
}

for (let i = 0 ; i < 24; i++) {
	if(i<10){
		i = "0"+i
	}
  hours.push(i)
}

for (let i = 0 ; i < 60; i++) {
	if(i<10){
		i = "0"+i
	}
  minutes.push(i)
}

	export default{
		data(){
			return{
				title: "添加提醒",
				timeShow: false,
				animationTime: {},
				timeLabels: [{
					title: "今天",
					status: false
				},{
					title: "明天",
					status: false
				},{
					title: "后天",
					status: false
				},{
					title: "下周",
					status: false
				},{
					title: "自定义",
					status: false
				}],
				years: years,
			    year: date.getFullYear(),
			    months: months,
			    month: "10",
			    days: days,
			    day: "02",
			    week: "周五",
			    hours: hours,
			    hour: "08",
			    minutes: minutes,
			    minute: "00",
			    value: [0, 0, 0, 0, 0],
			}
		},
		methods:{
			cancleBack(e){
				wx.navigateBack({
  					delta: 1
				})
			},
			saveBack(e){
				wx.showToast({
				  title: '保存成功！',
				  icon: 'none'
				})
				setTimeout(function(){
					wx.navigateBack({
	  					delta: 1
					})
				},2000)		
			},
			selectTime(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
		    	})

		      	this.animation = animation;
			   	animation.bottom(0).step();
		    	this.timeShow = true;
			   	this.animationTime = animation.export();

			},
			hideTime(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
		    	})

		      	this.animation = animation;
			   	animation.bottom('-100%').step();
		    	this.timeShow = false;
			   	this.animationTime = animation.export();
			},
			queryTime(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
		    	})

		      	this.animation = animation;
			   	animation.bottom('-100%').step();
		    	this.timeShow = false;
			   	this.animationTime = animation.export();

			   	console.log(timeIdx);
			   	if(timeIdx == [] || timeIdx.length == 0 || timeIdx == ""){

			   	}else{
			   		this.value = timeIdx;
				   	let _year = this.years[timeIdx[0]];
					this.month = this.months[timeIdx[1]];
					this.day = this.days[timeIdx[2]];
					this.hour = this.hours[timeIdx[3]];

					let datew = new Date(_year,this.month-1,this.day).getDay();
					switch(datew){
						case 1: datew = "周一";
						break;
						case 2: datew = "周二";
						break;
						case 3: datew = "周三";
						break;
						case 4: datew = "周四";
						break;
						case 5: datew = "周五";
						break;
						case 6: datew = "周六";
						break;
						default: datew = "周日";
					}
					console.log(datew);
					this.week = datew;
					this.minute = this.minutes[timeIdx[4]];
			   	}
			   	
			},
			bindChange(e){
				timeIdx = e.mp.detail.value;
			},
			remindChange(e){
				console.log(e.mp.detail)
			}
		},
    	onLoad(options) {
    		console.log(options.id);
    		if(options.id != undefined){
    			this.title = "修改提醒";
    		}else{
    			this.title = "添加提醒";
    		}
	    }
	}
</script>

<style scoped>
	#remindAdd{
		padding-top: 48px;
	}
	.remindAdd_box{
		padding: 10px 15px;
	}
	.remindAdd_box .edit_box:last-child{
		border-bottom: 0;
	}

	.time_box{
		display: inline-block;
		padding: 10px;
		background: #109dd8;
		color: #fff;
		font-size: 13px;
		margin-bottom: 15px;
	}
	.time_box span{
		margin-right: 8px;
	}
	.time_box img{
		display: block;
		float: right;
		width: 16px;
		height: 18px;
		margin-left: 25px;
	}

	.time_layer{
		width: 100%;
		background: #fff;
		position: fixed;
		left: 0;
		bottom: -100%;
		font-size: 13px;
		text-align: center;
		z-index: 10;
	}
	.time_top{
		padding: 15px 0;
		display: flex;
		justify-content: space-between;
		align-items: center;
		font-size: 13px;
		border-bottom: 1px solid #eee;
	}
	.t_left{
		color: #a6a6a6;
		width: 15%;
	}
	.t_right{
		color: #109dd8;
		width: 15%;
	}
	.time_top h2{
		font-size: 14px;
		color: #000;
	}
	.time_wrapper{
		background: rgba(0,0,0,.5);
	}
</style>