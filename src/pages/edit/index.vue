<template>
	<div id="edit">
		<div class="edit_header">
			<div class="back" @click="cancleBack">取消</div>
			<div class="header_title">{{title}}</div>
			<div class="save" @click="saveBack">保存</div>
		</div>
		<div class="edit_content">
			<div class="edit_box">
				<h3>跟进状态</h3>
				<ul>
					<li v-for="(item,index) in followLabels" :key="index" @click="selectFollow(index)" :class="item.status == true?'active':''">{{item.title}}</li>
				</ul>
			</div>
			<div class="edit_box">
				<h3>客户评级</h3>
				<ul>
					<li v-for="(item,index) in rateLabels" :key="index" @click="selectRate(index)" :class="item.status == true?'active':''">{{item.title}}</li>
				</ul>
			</div>
			<div class="edit_box">
				<h3>跟进日志</h3>
				<textarea name="log" placeholder="请输入跟进日志"></textarea>
			</div>
			<div class="edit_box">
				<div class="ipt_box"><input type="text" name="username" placeholder="请输入客户姓名"></div>
				<div class="ipt_box"><input type="text" name="company" placeholder="请输入公司简称"></div>
				<div class="ipt_box"><input type="text" name="remark" placeholder="请输入备注信息"></div>
			</div>			
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				title: "添加客户",
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
			}
		},
    	onLoad(options) {
    		console.log(options.phone);
    		if(options.phone != undefined){
    			this.title = options.phone;
    		}else{
    			this.title = "添加客户";
    		}
	    }
	}
</script>

<style scoped>
	#edit{
		padding-top: 48px;
	}

	.edit_content{
		padding: 10px 15px;
	}
	.edit_box .ipt_box{
		padding: 10px 15px;
		background: #fcfcfc;
		box-sizing: border-box;
		margin-bottom: 10px;
		border: 1px solid #E8E8E8;		
	}
	.edit_box input{
		display: block;
		width: 100%;
		color: #a6a6a6;
		background: #fcfcfc;
		font-size: 12px;
	}
	.edit_box:last-child{
		padding-top: 15px;
		border-bottom: 0;
	}
</style>