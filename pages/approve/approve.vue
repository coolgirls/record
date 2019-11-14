<template>
	<view class="content">
		<view class="approve-info">
			<view class="approve-item">
				<label class="name">姓名</label>
				<text class="info">{{detailInfo.Name}}</text>
			</view>
			<view class="approve-item">
				<label class="name">身份证号</label>
				<text class="info">{{detailInfo.IDCard}}</text>
			</view>
			<view class="approve-item">
				<label class="name">联系电话</label>
				<text class="info">{{detailInfo.Phone}}</text>
			</view>
			<view class="approve-item">
				<label class="name">银行卡号</label>
				<text class="info">{{detailInfo.CreditCardNumber}}</text>
			</view>
			<view class="approve-item">
				<label class="name">开户银行</label>
				<text class="info">{{detailInfo.OpeningBank}}</text>
			</view>
			<view class="approve-item">
				<label class="name">结款金额</label>
				<text class="info">{{detailInfo.Borrow}}</text>
			</view>
			<view class="approve-desc">
				<label class="name">备注</label>
				<textarea placeholder="备注" class="desc" v-model="Remark"></textarea>
			</view>
		</view>
		<view class="approve-btn">
			<view class="noAgree" @click="isAgree" :data-status="-1">不通过</view>
			<view class="agree" @click="isAgree" :data-status="1">通过</view>
		</view>
	</view>
</template>

<script>
	import qs from '../../qs.js'
	import webSite from '../../config.js'
	export default {
		data() {
			return {
				detailInfo:{},
				Remark:'',
				ID:''
			}
		},
		onLoad(options) {
			this.ID=options.id;
			uni.request({
				url:webSite.url+'AuditInfo/QueryAuditByID',
				data:{
					'ID':this.ID
				},
				header: {
					'Content-Type': 'application/x-www-form-urlencoded',
					'Accept':'application/json'
				},
				method: 'GET',
				success:(res)=>{
					console.log('审核信息',res);	
					if(res.data.code="0"){
						this.detailInfo=res.data.data;
					}else{
						uni.showToast({
							title:res.data.ErrMsg
						})
					}
				}
			})
		},
		methods: {
           isAgree(e){
			   var status=e.target.dataset.status;
			   var data={
				   'ID':this.ID,
				   'Status':status,
				   'Remark':this.Remark
			   }
			   uni.request({
			   	url:webSite.url+'AuditInfo/UpdateAudit',
			   	data:qs.stringify(data),
			   	header: {
			   		'Content-Type': 'application/x-www-form-urlencoded',
			   		'Accept':'application/json'
			   	},
			   	method: 'POST',
			   	success:(res)=>{
			   		console.log('是否通过',res);	
			   		if(res.data.Success){
			   			uni.navigateTo({
			   				url:'../approveList/approveList'
			   			})
			   		}else{
			   			uni.showToast({
			   				title:res.data.ErrMsg
			   			})
			   		}
			   	}
			   })
		   }
		}
	}
</script>

<style lang="less">
	.content {
		font-size:14px;
		.approve-info{
			.approve-item{
				display: flex;
				border-bottom:1px solid #f0eff5;
				height:80upx;
				line-height:80upx;
				label{
					width: 35%;
					display: flex;
					margin-left: 20px;
				}
				text{
					width: 65%;
					display: flex;
				}
			}
			.approve-desc{
				display: flex;
				label{
					width: 35%;
					display: flex;
					margin-left: 20px;
					margin-top: 20upx;
				}
				.desc{
					width: 60%;
					height: 240upx;
					margin-right: 5%;
					border: 1px solid #f0eff5;
					margin-top: 20upx;
					font-size: 14px;
					padding-left: 10upx;
					padding-top: 10upx;
				}
			}
		}
		.approve-btn{
			display: flex;
			margin:100upx 10%;
			.noAgree{
				width:45%;
				text-align: center;
				height: 70upx;
				line-height: 70upx;
				border: 1px solid #00b7ee;
				color: #00b7ee;
				border-radius: 8upx;
				margin-right: 10%;
			}
			.agree{
				width:45%;
				text-align: center;
				height: 70upx;
				line-height: 70upx;
				border: 1px solid #e51c23;
				color: #e51c23;
				border-radius: 8upx;
			}
		}
	}
</style>
