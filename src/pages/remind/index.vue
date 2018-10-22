<template>
	<div id="remind">
		<div class="remind_box">
			<div class="remind_item" v-for="(item,index) in remindLists" :key="index" @click.stop="noRemind(index)">
				<i-swipeout i-class="i-swipeout-demo-item" :actions="actions" :key="index" @change="swipeoutChange(item.id,$event)">
			        <view slot="content">
			        	<view class="i-swipeout-image">
			                <div class="circle_box" :style="{background: item.dot == true?item.background:'#dcdcdc'}" v-if="item.remind_status"><span v-if="item.dot"></span>{{item.week}}</div>
			                <div class="circle_box no" v-if="!item.remind_status"><img src="../../../static/images/no_remind.png"></div>
			           	</view>
				        <view class="i-swipeout-des">
			                <view class="i-swipeout-des-h2">{{item.date}}<span>{{item.week}} {{item.time}}</span></view>
			                <view class="i-swipeout-des-detail">{{item.info}}</view>
			           	</view>
			        </view>
			    </i-swipeout>
			</div>
			<i-divider content="没有更多数据了"></i-divider>
		</div>
		<div class="release" @click="addRemind">
			<a href=""><img src="../../../static/images/add.png"></a>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				toggle : false,
				actions: [
		            {
		                name: '不再提醒',
		                width: 70,
		                color: '#fff',
		                fontsize: '24',
		                background: '#bebebe'
		            },
		            {
		                name: '修改提醒',
		                width: 70,
		                color: '#fff',
		                fontsize: '24',
		                background: '#ed6b1d'
		            },
		            {
		                name: '删除提醒',
		                width: 70,
		                color: '#fff',
		                fontsize: '24',
		                background: '#e42828'
		            }
		        ],
		        remindLists:[
		        	{
		            	id: 1,
		        		remind_status: true,
		        		date: "12月13日",
		        		week: "周六",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#8acce7",
		        		dot: true
		        	},
		        	{
		            	id: 2,
		        		remind_status: true,
		        		date: "12月05日",
		        		week: "周五",
		        		time: "21:00",
		        		info: "提醒提醒提醒提醒",
		        		background: "#9ddaa1",
		        		dot: true
		        	},
		        	{
		            	id: 3,
		        		remind_status: true,
		        		date: "10月13日",
		        		week: "周四",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#e3ceaf",
		        		dot: true
		        	},
		        	{
		            	id: 4,
		        		remind_status: true,
		        		date: "10月05日",
		        		week: "周三",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#e6cfeb",
		        		dot: true
		        	},
		        	{
		            	id: 5,
		        		remind_status: true,
		        		date: "9月13日",
		        		week: "周六",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#8acce7",
		        		dot: false
		        	},
		        	{
		            	id: 6,
		        		remind_status: true,
		        		date: "9月13日",
		        		week: "周六",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#8acce7",
		        		dot: false
		        	},
		        	{
		            	id: 7,
		        		remind_status: false,
		        		date: "9月13日",
		        		week: "周六",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#8acce7",
		        		dot: false
		        	},
		        	{
		            	id: 8,
		        		remind_status: false,
		        		date: "9月13日",
		        		week: "周六",
		        		time: "21:00",
		        		info: "吾问无为谓",
		        		background: "#8acce7",
		        		dot: false
		        	}
		        ]
			}
		},
		methods:{
			swipeoutChange(id,e){
				let index = e.mp.detail.index
				console.log(id,index)
				if(index == 0){
					console.log("不再提醒！");
					let _url = "../remind/main?id="+index;
					wx.reLaunch({ url: _url });
				}
				else if(index == 1){
					let _url = "../remindAdd/main?id="+id;
					wx.navigateTo({ url: _url });
				}else{
					console.log("删除提醒！");
					let _url = "../remind/main?id="+index;
					wx.reLaunch({ url: _url });
				}
			},
			addRemind(e){
				let url = "../remindAdd/main";
				wx.navigateTo({ url });
			},
			noRemind(index){
				let _url = "../remindEdit/main?id="+index;
				wx.navigateTo({ url: _url });
			}
		},
    	onLoad() {

	    }
	}
</script>

<style scoped>
	.remind_box{
		overflow: hidden;
		padding: 0 15px;
	}
	.remind_item{
		overflow: hidden;
		border-bottom: 1px solid #F4F4F4;
	}
	.i-swipeout-image{
		float: left;
		width: 15%;
	}
	.i-swipeout-image .circle_box{
		width: 42px;
		height: 42px;
		border-radius: 50%;
		color: #fff;
		font-size: 13px;
		display: flex;
		align-items: center;
		justify-content: center;
		position: relative;
	}
	.i-swipeout-image .circle_box span{
		display: block;
		position: absolute;
		width: 8px;
		height: 8px;
		border-radius: 50%;
		background: #e42828;
		right: 6px;
		top: 0;
	}
	.i-swipeout-image .circle_box.no{
		background: #dcdcdc;		
	}
	.i-swipeout-image .circle_box img{
		display: block;
		width: 20px;
		height: 20px;
	}
	.i-swipeout-des-h2{
		color: #828282;
		font-size: 14px;
		margin-bottom: 5px;
	}
	.i-swipeout-des-h2 span{
		margin-left: 10px;
	}
	.i-swipeout-des-detail{
		color: #303030;
		font-size: 13px;
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}
</style>