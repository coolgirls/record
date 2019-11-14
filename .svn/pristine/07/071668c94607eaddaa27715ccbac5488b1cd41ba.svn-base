<template>
	<view class="content">
		<view class="logo">
			<image src="../../static/logo.png"></image>
		</view>
		<view class="login-list">
			<view class="list-item">
				<input placeholder="请输入账号" v-model="UserName"/>
			</view>
			<view class="list-item">
				<input placeholder="请输入密码" v-model="PassWord" password/>
			</view>
		</view>
		<view class="login-btn" @click="goApprove">登录</view>
	</view>
</template>

<script>
	import qs from '../../qs.js'
	import webSite from '../../config.js'
	export default {
		data() {
			return {
				UserName:'',
				PassWord:''
			}
		},
		onLoad() {

		},
		methods: {
           goApprove(){
			   var UserName=this.UserName;
			   var PassWord=this.PassWord;
			   var data={
				   'UserName':UserName,
				   'PassWord':PassWord
			   }
			   uni.showLoading({
			   	title:'登录中...'
			   })
			   uni.request({
			   	url:webSite.url+'UserInfo/Login',
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
						uni.showToast({
							title:'登录成功',
							duration: 2000,
							icon:"success",
							success:(res)=>{
								setTimeout(function(){
									uni.navigateTo({
										url:'../approveList/approveList?type=0'
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
		.logo{
			width: 200upx;
			height: 200upx;
			margin: 100upx auto;
			image{
				width: 100%;
				height: 100%;
			}
		}
        .login-list{
			width:62%;
			margin:0 auto;
			.list-item{
				border-bottom: 1px solid #00b7ee;
				margin-bottom: 48upx;
				height: 70upx;
			}
		}
		.login-btn{
			background: #00b7ee;
			color: #fff;
			width: 62%;
			height: 100upx;
			text-align: center;
			line-height: 100upx;
			margin:80upx auto 40upx;
			border-radius: 10upx;
		}
	}
</style>
