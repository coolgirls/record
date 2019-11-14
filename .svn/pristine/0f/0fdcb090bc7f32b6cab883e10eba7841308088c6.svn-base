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
				<textarea placeholder="备注" class="desc"></textarea>
			</view>
		</view>
	</view>
</template>

<script>
	import webSite from '../../config.js'
	export default {
		data() {
			return {
				detailInfo:{}
			}
		},
		onLoad(options) {
          console.log('op',options);
		     uni.request({
		     	url:webSite.url+'AuditInfo/QueryAuditByID',
		     	data:{
					'ID':options.id
				},
		     	header: {
		     		'Content-Type': 'application/x-www-form-urlencoded',
		     		'Accept':'application/json'
		     	},
		     	method: 'GET',
		     	success:(res)=>{
		     		console.log('详情',res);	
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
					margin-top: 20upx;
					font-size: 14px;
				}
			}
		}
	}
</style>
