<template>
	<view class="content">
		<view class="banner">
			<image src="../../static/banner.png"></image>
		</view>
		<view class="approve-list">
			<view class="list-item">
				<view class="item-left">
					<label class="name">单位名称</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写单位名称" v-model="CompanyName"/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">姓名</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写姓名" v-model="Name"/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">身份证号</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写身份证号" v-model="IDCard "/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">联系电话</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写联系电话" v-model="Phone"/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">银行卡号</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写银行卡号" v-model="CreditCardNumber"/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">开户银行</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="text" placeholder="请填写开户银行" v-model="OpeningBank"/>
				</view>
			</view>
			<view class="list-item">
				<view class="item-left">
					<label class="name">借款金额</label>
					<text class="red">*</text>
				</view>
				<view class="item-right">
					<input type="number" placeholder="请填写借款金额"  v-model="Borrow"/>
				</view>
			</view>
		</view>
		<view class="approve-btn" @click="login">提交申请</view>
	</view>
</template>

<script>
	import qs from '../../qs.js'
	import webSite from '../../config.js'
	export default {
		data() {
			return {
				'CompanyName':'',
				'Name':'',
				'IDCard':'',
				'Phone':'',
				'CreditCardNumber':'',
				'OpeningBank':'',
				'Borrow':''
			}
		},
		onLoad() {

		},
		methods: {
           login(){
			   var CompanyName=this.CompanyName;
			   var Name=this.Name;
			   var IDCard=this.IDCard;
			   var Phone=this.Phone;
			   var CreditCardNumber=this.CreditCardNumber;
			   var OpeningBank=this.OpeningBank;
			   var Borrow=this.Borrow;
			   var data={
				   'CompanyName':CompanyName,
				   'Name':Name,
				   'IDCard':IDCard,
				   'Phone':Phone,
				   'CreditCardNumber':CreditCardNumber,
				   'OpeningBank':OpeningBank,
				   'Borrow':Borrow
			   }
			   uni.showLoading({
			   	title:'申请中...'
			   })
			   uni.request({
			   	url:webSite.url+'AuditInfo/AddAudit',
			   	data:qs.stringify(data),
			   	header: {
			   		'Content-Type': 'application/x-www-form-urlencoded',
					'Accept':'application/json'
			   	},
			   	method: 'POST',
			   	success:(res)=>{
					uni.hideLoading();
			   		console.log('res',res);	
					if(res.data.Success){
						uni.setStorageSync('name',Name);
						uni.setStorageSync('phone',Phone);
						uni.showToast({
							title:'申请成功',
							duration: 2000,
							icon:"success",
							success:(res)=>{
								setTimeout(function(){
									uni.navigateTo({
										url:'../approveList/approveList?type=1'
									})
								},2000)
							}
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
		.banner{
			width: 750upx;
			height: 273upx;
			image{
				width: 100%;
				height: 100%;
				display: block;
			}
		}
        .approve-list{
			.list-item{
				display: flex;
				background:rgba(0,183,238,5%);
				margin-bottom:20upx;
				padding:24upx;
				border-radius:20upx;
				.item-left{
					display: flex;
					width:30%;
					.red{
						color: #f00;
					}
				}
				.item-right{
					.uni-input-placeholder{
						font-size: 14px;
					}
				}
			}
		}
		.approve-btn{
			background: #00b7ee;
			color: #fff;
			width: 80%;
			height: 100upx;
			text-align: center;
			line-height: 100upx;
			margin:80upx auto 40upx;
			border-radius: 10upx;
		}
	}
</style>
