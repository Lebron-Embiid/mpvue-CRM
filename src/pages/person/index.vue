<template>
	<div id="person">
		<div class="person_header">
			<div class="img"><img :src="user_head"></div>
			<h3>{{username}}</h3>
		</div>
		<div class="person_nav">
			<div class="nav_item" @click="toNav(index)" v-for="(item,index) in navLists" :key="index">
				<img :src="item.icon" class="n_icon">
				<p>{{item.title}}<span>{{item.num}}</span></p>
				<img src="../../../static/images/right.png" class="n_right">
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				user_head: require("../../../static/images/my_head.png"),
				username: "吾问无为谓",
				navLists:[
					{
						icon: require("../../../static/images/my_icon1.png"),
						title: "公海资源",
						num: "2231个"
					},
					{
						icon: require("../../../static/images/my_icon2.png"),
						title: "呼叫任务",
						num: "529个"
					},
					{
						icon: require("../../../static/images/my_icon3.png"),
						title: "我的客户",
						num: ""
					}
				]
			}
		},
		methods:{
			toNav(index){
				console.log(index)
				switch (index) {
					case 0:
						// statements_1
					    var url = '../resource/main';
					    wx.navigateTo({ url });
						break;
					case 1:
						// statements_1
					    var url = '../task/main';
					    wx.navigateTo({ url });						
						break;
					default:
						// statements_def
					    var url = '../client/main';
					    wx.reLaunch({ url });
						break;
				}
			}
		},
    	onLoad() {

	    }
	}
</script>

<style scoped>
	.person_header{
		text-align: center;
		background: #fff;
		border-bottom: 10px solid #f7f7f7;
	}
	.person_header .img{
		display: block;
		width: 57.5px;
		height: 57.5px;
		border-radius: 50%;
		margin: 15px auto 5px;
	}
	.person_header .img img{
		display: block;
		width: 100%;
		height: 100%;
		border-radius: 50%;
	}
	.person_header h3{
		color: #303030;
		font-size: 16px;
		padding-bottom: 15px;
		border-bottom: 1px solid #DFDFDF;
	}
	.person_nav{
		overflow: hidden;
		padding: 10px 15px;
		border-top: 1px solid #E8E8E8;
	}
	.nav_item{
		overflow: hidden;
		padding: 20px 0 10px;
		border-bottom: 1px solid #E7E7E7;
		display: flex;
		justify-content: space-between;
	}
	.nav_item .n_icon{
		display: inline-block;
		width: 22.5px;
		height: 19px;
		vertical-align: middle;
	}
	.nav_item p{
		width: 85%;
		color: #303030;
		font-size: 14px;
		padding-right: 10px;
		box-sizing: border-box;
	}
	.nav_item p span{
		float: right;
		color: #8f8f8f;
		font-size: 12px;
	}
	.nav_item .n_right{
		float: right;
		width: 9.5px;
		height: 17px;
	}
</style>