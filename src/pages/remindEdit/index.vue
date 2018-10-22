<template>
	<div id="remindEdit">
		<div class="remindEdit_box">
			<div class="remind_item">
				<h4>提醒时间</h4>
				<p>{{date}} {{week}} {{time}}</p>
			</div>
			<div class="remind_item">
				<h4>提醒内容</h4>
				<p>{{content}}</p>
			</div>
			<button class="no_remind" :class="remindActive == true?'active':''" @click="clickNoRemind">不再提醒</button>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				date: "10月13日",
				week: "周六",
				time: "20：00",
				content: "为了让更多的潜在用户能够更好的关注到公司网站的内容，那么保持企业网站一定的鲜活度是十分有必要的。",
				remindActive: false
			}
		},
		methods:{
			clickNoRemind(e){
				this.remindActive = true
			}
		},
    	onLoad(options) {
    		console.log(options.id);
	    }
	}
</script>

<style scoped>
	.remindEdit_box{
		padding: 5px 15px;
	}
	.remind_item{
		padding: 20px 0 15px;
		border-bottom: 1px solid #EBEBEB;
	}
	.remind_item h4{
		color: #646464;
		font-size: 13px;
		margin-bottom: 5px;
	}
	.remind_item p{
		color: #373737;
		font-size: 12px;
	}
	.no_remind{
		width: 60%;
		height: 35px;
		background: #109dd8;
		color: #fff;
		font-size: 13px;
		border: 0;
		border-radius: 0;
		outline: none;
		margin: 100px auto;
	}
	.no_remind.active{
		/*opacity: .8;*/
		background: #818181;
	}
</style>