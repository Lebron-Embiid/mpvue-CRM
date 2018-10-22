<template>
	<div id="number">
		<div class="number_top">
			<h2>{{number}}</h2>
			<p>{{address}}</p>
			<ul>
				<li @click="toRemindEdit"><img src="../../../static/images/number_icon1.png"></li>
				<li @click="toEdit"><img src="../../../static/images/number_icon2.png"></li>
				<li @click="toCall"><img src="../../../static/images/number_icon3.png"></li>
			</ul>
		</div>
		<div class="nummber_content">
			<div class="n_title">跟进状态：{{status}}</div>
			<div class="n_box">
				<span class="till">通话记录</span>
				<ul>
					<li v-for="(item,index) in callRecords" :key="index">{{item.date}}<span>{{item.week}}</span><span>{{item.time}}</span><span>{{item.type}}</span></li>
				</ul>
			</div>
			<div class="n_title">客户评级：{{rate}}</div>
			<div class="n_box">
				<span class="till">跟进日志</span>
				<ul>
					<li v-for="(item,index) in logLists" :key="index">
						<h4>{{item.time}}</h4>
						<p>{{item.info}}</p>
					</li>
				</ul>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				number: "075561885188",
				address: "归属地未知",
				status: "报价",
				rate: "一星",
				callRecords: [{
					date: "10月12日",
					week: "周四",
					time: "11:22",
					type: "未接"
				},{
					date: "10月12日",
					week: "周四",
					time: "11:22",
					type: "未接"
				}],
				logLists: [{
					time: "10月12日",
					info: "打造企业全网营销的品牌社交生态链让网站与营销相结合；让移动与营销相结合；让社交与移动相结合"
				},{
					time: "10月12日",
					info: "打造企业全网营销的品牌社交生态链让网站与营销相结合；让移动与营销相结合；让社交与移动相结合"
				}]
			}
		},
		methods:{
			toRemindEdit(e){
				let url = "../remindEdit/main";
				wx.navigateTo({ url });
			},
			toEdit(e){
				let url = "../edit/main?phone="+this.number;
				wx.navigateTo({ url });
			},
			toCall(e){
				wx.makePhoneCall({
			        phoneNumber: this.number,
			        success: function(res){
			        	console.log(res)
			        },
			        fail: function(res){
			         	console.log(res)
			        }
			    })
			}
		},
    	onLoad() {

	    }
	}
</script>

<style scoped>
	.number_top{
		padding: 45px 15px 30px;
		background: #109dd8;
		text-align: center;
	}
	.number_top h2{
		color: #feffff;
		font-size: 24px;
		margin: 0;
	}
	.number_top p{
		color: #b4e9ff;
		font-size: 13px;
		margin: 5px 0 15px;
	}
	.number_top ul{
		display: flex;
		justify-content: space-around;
	}
	.number_top ul li{
		width: 54px;
		height: 54px;
		background: #fff;
		border-radius: 50%;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	.number_top ul li:active{
		background: rgba(255,255,255,.8);
	}
	.number_top ul li img{
		display: block;
		width: 27px;
		height: 27px;
	}

	.n_title{
		color: #5a5a5a;
		font-size: 14px;
		padding: 15px 15px 10px;
		border-top: 1px solid #EAEAEA;
		border-bottom: 1px solid #EAEAEA;
		background: #fcfcfc;
	}
	.n_box{
		padding: 20px 15px 15px;
	}
	.n_box .till{
		display: inline-block;
		padding: 8px 15px;
		color: #5a5a5a;
		font-size: 13px;
		border: 1px solid #EAEAEA;
		border-radius: 5px;
	}
	.n_box ul li{
		padding: 15px 0;
		border-bottom: 1px solid #EFEFEF;
		color: #5a5a5a;
		font-size: 13px;
	}
	.n_box ul li:last-child{
		border-bottom: 0;
	}
	.n_box ul li span{
		margin-left: 8px;
	}
	.n_box ul li h4{
		color: #434343;
		font-size: 14px;
		margin-bottom: 10px;
	}
	.n_box ul li p{
		color: #5a5a5a;
		font-size: 12px;
		line-height: 1.6;
	}
</style>