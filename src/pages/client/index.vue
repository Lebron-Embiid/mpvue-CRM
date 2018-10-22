<template>
	<div id="client">
		<div class="top_header">
			客户数：{{clientNum}} 
			<div @click="showFilter"><img src="../../../static/images/filter.png" alt=""><span>筛选</span></div>
		</div>
		<div class="client_box">
			<div class="client_item" v-for="(item,index) in clientLists" :key="index" @longpress="longClick(index)" @click="toNumber(item.id)">
				<div class="box">
					<div class="c_head">
						<div :style="{background: item.bgColor}"><img :src="item.head_img"></div>
					</div>
					<div class="c_content">
						<h3>{{item.phone}} <span><img src="../../../static/images/star.png" v-for="(i,idx) in item.starNum" :key="idx"></span></h3>
						<p>{{item.address}} <span class="c_com">{{item.company}}</span> <span class="c_status" :style="{color: item.color}">{{item.status}}</span></p>
					</div>
				</div>
				<div class="c_layer" v-show="item.layerActive">
					<h4>删除客户</h4>
					<h5>您确认要删除 {{item.phone}} 吗？</h5>
					<p><span class="cancle" @click.stop="hideLayer">取消</span><span class="ok" @click.stop="Client_del(index)">确定</span></p>
				</div>
			</div>
			<i-divider content="没有更多数据了"></i-divider>
		</div>
      	<div class="call_layer" v-show="layerShow" @click="hideLayer"></div>
		<div class="release" @click="addClient">
			<a href=""><img src="../../../static/images/add.png"></a>
		</div>
		<div class="filter_wrapper" v-show="filterShow" @click="hideFilter"></div>
		<div class="filter_layer" :animation="animationFilter">
			<div class="filter_top">
				<span class="f_cancle" @click="hideFilter">取消</span>
				<span class="f_ok" @click="okFilter">确定</span>
			</div>
			<div class="f_content">
				<div class="label_box">
					<h3>跟进状态</h3>
					<ul>
						<li v-for="(item,index) in followLabels" :key="index" @click="selectFollow(index)" :class="item.status == true?'active':''">{{item.title}}</li>
					</ul>
				</div>
				<div class="label_box">
					<h3>客户评级</h3>
					<ul>
						<li v-for="(item,index) in rateLabels" :key="index" @click="selectRate(index)" :class="item.status == true?'active':''">{{item.title}}</li>
					</ul>
				</div>
				<div class="key_words">
					<h3>关键字</h3>
					<input type="text" placeholder="请输入公司名称、客户名称、电话号码" name="search_key">
					<div class="key_btn">
						<button class="reset_btn">重置</button>
						<button>搜索</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				clientNum: 8,
				layerShow: false,
				filterShow: false,
				animationFilter: {},
				clientLists:[{
					id: 1,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#8acce7",
					phone: "15814720561",
					starNum: 3,
					address: "广东深圳移动",
					company: "某某某科技有限公司",
					status: "意向",
					color: "#ca0505",
					layerActive: false
				},{
					id: 2,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#9cdaa1",
					phone: "15814720561",
					starNum: 1,
					address: "广东深圳移动",
					company: "",
					status: "初防",
					color: "#804a03",
					layerActive: false
				},{
					id: 3,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#e3ceaf",
					phone: "15174318603",
					starNum: 2,
					address: "广东深圳移动",
					company: "",
					status: "报价",
					color: "#009bdb",
					layerActive: false
				},{
					id: 4,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#e5cfea",
					phone: "17681545208",
					starNum: 3,
					address: "广东深圳移动",
					company: "某某某科技有限公司",
					status: "成交",
					color: "#31ba01",
					layerActive: false
				},{
					id: 5,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#8acce7",
					phone: "15814720561",
					starNum: 3,
					address: "广东深圳移动",
					company: "某某某科技有限公司",
					status: "意向",
					color: "#ca0505",
					layerActive: false
				},{
					id: 6,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#9cdaa1",
					phone: "15814720561",
					starNum: 1,
					address: "广东深圳移动",
					company: "",
					status: "初防",
					color: "#804a03",
					layerActive: false
				},{
					id: 7,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#e3ceaf",
					phone: "15174318603",
					starNum: 2,
					address: "广东深圳移动",
					company: "",
					status: "报价",
					color: "#009bdb",
					layerActive: false
				},{
					id: 8,
					head_img: require("../../../static/images/default_person.png"),
					bgColor: "#e5cfea",
					phone: "17681545208",
					starNum: 3,
					address: "广东深圳移动",
					company: "某某某科技有限公司",
					status: "成交",
					color: "#31ba01",
					layerActive: false
				}],
				followLabels:[{
					title: "未标记",
					status: false
				},{
					title: "初访",
					status: false
				},{
					title: "意向",
					status: false
				},{
					title: "报价",
					status: false
				},{
					title: "成交",
					status: false
				}],
				rateLabels:[{
					title: "无星",
					status: false
				},{
					title: "一星",
					status: false
				},{
					title: "二星",
					status: false
				},{
					title: "三星",
					status: false
				}]
			}
		},
		methods:{
			longClick(index){
				console.log(index)
				this.layerShow = true;
				for(var i in this.clientLists){
					this.clientLists[i].layerActive = false
				}
				this.clientLists[index].layerActive = true
			},
			toNumber(id){
				console.log(id);
				let url = "../number/main?id="+id;
				wx.navigateTo({ url })
			},
			hideLayer(e){
				this.layerShow = false;
				for(var i in this.clientLists){
					this.clientLists[i].layerActive = false
				}
			},
			Client_del(index){
				this.layerShow = false;
				console.log("删除！"+index)
				this.clientLists[index].layerActive = false
			},
			showFilter(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
			    })

			    this.animation = animation;
			    animation.bottom(0).step();
			    this.filterShow = true;
			    this.animationFilter = animation.export();
			},
			hideFilter(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
			    })

			    this.animation = animation;
			    animation.bottom('-100%').step();
			    this.filterShow = false;
			    this.animationFilter = animation.export();
			},
			okFilter(e){
				var animation = wx.createAnimation({
			        transformOrigin: "50% 50%",
			        duration: 300,
			        timingFunction: 'ease',
			        delay: 0
			    })

			    this.animation = animation;
			    animation.bottom('-100%').step();
			    this.filterShow = false;
			    this.animationFilter = animation.export();
			    console.log("确定");
			},
			selectFollow(index){
				console.log(index);
				// for(var j in this.followLabels){
				// 	this.followLabels[j].status = false;
				// }
				if(this.followLabels[index].status == true){
					this.followLabels[index].status = false;
				}else{
					this.followLabels[index].status = true;
				}
			},
			selectRate(index){
				console.log(index);
				// for(var x in this.rateLabels){
				// 	this.rateLabels[x].status = false;
				// }
				if(this.rateLabels[index].status == true){
					this.rateLabels[index].status = false;
				}else{
					this.rateLabels[index].status = true;
				}
			},
			addClient(e){
				let url = "../edit/main";
				wx.navigateTo({ url });				
			}
		},
    	onLoad() {

	    }
	}
</script>

<style scoped>
	#client{
		padding-bottom: 50px;
	}
	.top_header{
		overflow: hidden;
		padding: 15px 15px 10px;
		border-bottom: 1px solid #F6F6F6;
		color: #828282;
		font-size: 14px;
	}
	.top_header div{
		float: right;
	}
	.top_header div img{
		display: inline-block;
		width: 17.5px;
		height: 15.5px;
		vertical-align: middle;
		margin: 0 5px 2px 0;
	}

	.client_box{
		/*overflow: hidden;*/
		padding: 0 15px;
	}
	.client_item{
		padding: 15px 0;
		border-bottom: 1px solid #F8F8F8;
		position: relative;
	}
	.client_item .box{
		overflow: hidden;
	}
	.c_layer{
		position: absolute;
		right: 15px;
		top: 50px;
		background: #fff;
		z-index: 9;
		padding: 15px 10px;
		box-shadow: 0 0 5px #f0f0f0;
		text-align: center;
		color: #000;
		font-size: 13px;
	}
	.c_layer h4{
		margin-bottom: 10px;
	}
	.c_layer h5{
		margin-bottom: 20px;
	}
	.c_layer p{
		overflow: hidden;
		padding: 0 15px;
	}
	.c_layer p .cancle{
		float: left;
	}
	.c_layer p .ok{
		float: right;
		color: #dd1616;
	}
	.c_head{
		width: 15%;
		float: left;
	}
	.c_head div{
		width: 42px;
		height: 42px;
		border-radius: 50%;
	}
	.c_head div img{
		display: block;
		width: 100%;
		height: 100%;
		border-radius: 50%;
	}
	.c_content{
		width: 85%;
		float: right;
	}
	.c_content h3{
		color: #282828;
		font-size: 16px;
		margin-bottom: 5px;
	}
	.c_content h3 span{
		float: right;
	}
	.c_content h3 span img{
		display: inline-block;
		width: 14.5px;
		height: 13.5px;
		margin-left: 2px;
		vertical-align: middle;
	}
	.c_content p{
		color: #828282;
		font-size: 13px;
	}
	.c_content p .c_com{
		margin-left: 20px;
	}
	.c_content p .c_status{
		float: right;
	}

	.filter_wrapper{
		background: rgba(0,0,0,.1);
	}
	.filter_layer{
		position: fixed;
		width: 100%;
		left: 0;
		bottom: -100%;
		background: #fff;
		z-index: 12;
	}
	.filter_top{
		overflow: hidden;
		padding: 15px 15px 10px;
		border-bottom: 1px solid #E8E8E8;
	}
	.filter_top span{
		display: inline-block;
	}
	.f_cancle{
		color: #8d8d8d;
		font-size: 14px;
		float: left;
	}
	.f_ok{
		float: right;
		color: #109dd8;
		font-size: 14px;
		text-align: right;
	}
	.f_content{
		overflow: hidden;
		padding: 0 15px 35px;
	}
	.label_box{
		padding-bottom: 5px;
		border-bottom: 1px solid #ECECEC;
	}
	.label_box h3,.key_words h3{
		color: #000;
		font-size: 13px;
		margin: 15px 0 10px;
	}
	.label_box ul{
		overflow: hidden;
		display: flex;
		justify-content: space-between;
		flex-wrap: wrap;
	}
	.label_box ul li{
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
	.label_box ul li.active{
		color: #109dd8;
		border-color: #109dd8;
	}
	.key_words input{
		border: 1px solid #ECECEC;
		background: #fcfcfc;
		color: #a6a6a6;
		font-size: 12px;
		outline: none;
		padding: 10px 10px 8px 15px;
		margin-bottom: 35px;
	}
	.key_btn{
		display: flex;
		justify-content: space-around;
	}
	.key_btn button{
		width: 103px;
		height: 35px;
		color: #fff;
		font-size: 13px;
		background: #109dd8;
		border: 0;
		border-radius: 0;
	}
	.key_btn .reset_btn{
		background: #aaddf3;
	}
	.key_btn button:active{
		opacity: .8;
	}
</style>