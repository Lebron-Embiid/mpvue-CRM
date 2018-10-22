<template>
	<div id="task">
		<div class="task_box">
			<div class="task_item" @click="callPhone(index)" v-for="(item,index) in taskLists" :key="index">
				<h3>{{item.phone}} <span :class="item.status == true?'active':''">{{item.type}}</span></h3>
				<p>{{item.name}} <span>{{item.time}}</span></p>
			</div>
		</div>
	</div>
</template>

<script>
	export default{
		data(){
			return{
				taskLists:[
					{
						phone: "1336896589",
						type: "已拨打",
						name: "姓名未知",
						time: "1小时前",
						status: false
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "3小时前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "15小时前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "一天前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "两天前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "3小时前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "15小时前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "一天前",
						status: true
					},
					{
						phone: "1336896589",
						type: "未拨打",
						name: "姓名未知",
						time: "两天前",
						status: true
					}
				]
			}
		},
		methods:{
			callPhone(index){
				console.log(index)
				wx.makePhoneCall({
		        	phoneNumber: this.taskLists[index].phone,
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
	.task_box{
		overflow: hidden;
		padding: 0 15px;
	}
	.task_item{
		overflow: hidden;
		padding: 15px 0 10px;
		border-bottom: 1px solid #EBEBEB;
	}
	.task_item:last-child{
		border-bottom: 0;
	}
	.task_item h3{
		color: #282828;
		font-size: 16px;
		margin-bottom: 5px;
	}
	.task_item h3 span{
		color: #828282;
		font-size: 13px;
		float: right;
	}
	.task_item h3 span.active{
		color: #dd0d0d;
	}
	.task_item p{
		color: #828282;
		font-size: 13px;
	}
	.task_item p span{
		color: #828282;
		font-size: 12px;
		float: right;
	}
</style>