<template>
	<div id="resource">
		<div class="res_box">
			<div class="res_item" v-for="(item,index) in resourceLists" :key="index">
				<div class="res_left">
					<h3>{{item.phone}}</h3>
					<p>{{item.time}}</p>
				</div>
				<div class="res_right">
					<button :class="item.status == true?'active':''" @click="receiveRes(index)">领取</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				resourceLists:[
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					},
					{
						phone: "158****0561",
						time: "15小时前",
						status: false
					}
				]
			}
		},
		methods:{
			receiveRes(index){
				console.log(index)
				if(this.resourceLists[index].status == true){
					wx.showToast({
						title: '您已领取过了！',
						icon: 'none'
					})
				}else{
					wx.showToast({
						title: '领取成功!',
						icon: 'none'
					})
				}
				this.resourceLists[index].status = true
			}
		},
    	onLoad() {

	    }
	}
</script>

<style scoped>
	.res_box{
		overflow: hidden;
		padding: 0 15px;
	}
	.res_item{
		padding: 15px 0 10px;
		border-bottom: 1px solid #F8F8F8;
		display: flex;
		align-items: center;
		justify-content: space-between;
	}
	.res_left h3{
		color: #282828;
		font-size: 16px;
		margin-bottom: 5px;
	}
	.res_left p{
		color: #828282;
		font-size: 13px;
	}
	.res_right button{
		display: block;
		width: 69px;
		height: 31.5px;
		color: #fff;
		font-size: 13px;
		border-radius: 5px;
		background: #009bdb;
	}
	.res_right button.active{
		background: #a0a0a0;
	}
</style>